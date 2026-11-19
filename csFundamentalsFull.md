# CS Fundamentals

## chapter 1 Processes and threads

- a process = a running program with its own memory
- a thread = a path of execution inside a process. threads in one process share the memory
- Node runs our JavaScript on one main thread. the libuv thread pool does some file and DNS work beside it
- a second Nest process is a second process. it does not share the JavaScript heap
- a crash in one process does not wipe the other's heap. a bug in a shared thread can
- `fork` on a Unix machine copies a process. the child starts as a copy and can then replace itself with another program

```ts
// one thread: this loop blocks every request on this process
let n = 0;
for (let i = 0; i < 1_000_000_000; i++) n++;
```

- the event loop is how one thread still handles many sockets. it waits for I/O. it does not wait inside that for-loop
- PM2 runs more than one process when we ask it to. they share nothing but the port, through the OS

- homework of chapter 1
```ts
// 1a  process or thread: two Prisma clients in two Node processes
// 1b  why a billion-iteration loop freezes every request on that process
// 1c  what the threads inside one process can both see
```

## chapter 2 Context switching and CPU scheduling

- a context switch = the CPU stops one thread and resumes another
- it saves registers and the stack pointer, then loads the other thread's
- it is not free. a machine that switches all day does less work
- the scheduler decides who runs
- a time slice = the turn a thread gets before the scheduler may switch
- FIFO runs jobs in arrival order. a long job blocks a short one
- round robin gives each job a slice, then the next job
- priority runs the higher priority first. a low priority job can starve if we never age it
- our Node process is one of those jobs. the OS schedules it beside nginx and Postgres

```text
jobs A=10ms, B=1ms, one CPU
FIFO if A arrived first: A finishes at 10, B at 11
round robin slice 1ms: B can finish near the start, A finishes a little later
```

- we do not write the scheduler. we write work that yields. a tight loop does not yield
- I/O wait is a natural yield. the CPU can run someone else while Postgres reads disk

- homework of chapter 2
```text
// 2a  three jobs of 4ms, 1ms, 1ms. FIFO versus a 1ms round robin. when does the short job finish
// 2b  what is saved on a context switch
// 2c  why a priority queue without aging can leave a job waiting forever
```

## chapter 3 Concurrency, locks, and deadlocks

- concurrency = more than one thing in progress
- it is not the same as parallel. parallel means two things run at the same instant, on two cores
- Node is concurrent on one thread. two requests interleave at every await
- a lock = one holder at a time. in Postgres it is a row lock. in a process it is a mutex
- a race = two readers both see 10, both write 11
- the fix in SQL is one UPDATE that uses the old value
- deadlock = A holds 1 and wants 2. B holds 2 and wants 1. nobody moves
- the conditions are mutual exclusion, hold and wait, no preemption, and a circle
- break the circle. take locks in a fixed order. or let the database kill one transaction and retry

```ts
// both requests read, both await, both write. the await is the gap
const row = await db.counter.findUnique({ where: { id: 1 } });
await db.counter.update({ where: { id: 1 }, data: { n: row.n + 1 } });
```

```sql
UPDATE counters SET n = n + 1 WHERE id = 1;
```

- the first snippet loses updates. the SQL statement does not
- two Prisma transactions that lock match A then match B, and the other locks B then A, can deadlock. lock by id order

- homework of chapter 3
```sql
-- 3a  rewrite the lost increment as one statement
-- 3b  name the four deadlock conditions in a sentence
-- 3c  lock order for two match rows m_2 and m_1
```

## chapter 4 Memory and virtual memory

- a process sees virtual addresses. the CPU and the OS map them to physical frames
- a page = a fixed block of that virtual space. often 4 KB
- a page fault = the page is not in RAM. the OS loads it from disk, or the process crashes if the address was never valid
- swapping = moving a page out to disk because RAM is full. the machine gets slow before it gets wrong
- a leak = we keep allocating and never drop the reference. the process RSS grows
- in Node, a global Map that we never delete is a leak
- the stack holds the current function's locals. the heap holds objects that outlive the function
- RSS is the resident set, the physical memory the process is using now

```ts
const cache = new Map<string, string>();
function remember(id: string, body: string) {
  cache.set(id, body); // fine until this map is the whole history of the site
}
```

- a page table is the map from virtual page to frame
- two processes can map a file into memory. that is a shared mapping. our Nest processes do not need it. they talk over HTTP or Redis

- homework of chapter 4
```ts
// 4a  stack or heap: the array we return from a function
// 4b  what a page fault means
// 4c  a Map in a module scope that stores every request body. what happens over a week
```

## chapter 5 File systems and system calls

- a file system = the way the disk becomes files and folders
- an inode = the record of a file. name is in the directory. the inode holds size, permissions, and where the blocks are
- a directory is a file whose contents are names and inode numbers
- deleting a name does not always free the blocks. they free when the last name and the last open handle are gone
- a system call = the door from our program into the kernel
- open, read, write, close, socket, bind, fork are system calls
- we rarely type them. Node calls them for us. a slow API is sometimes a slow read underneath
- permissions are owner, group, other, and read, write, execute

```text
open("stream.m3u8") -> a file descriptor, a small integer
read(fd, buffer)
close(fd)
```

- a file descriptor is per process. fd 1 is usually stdout
- nginx reading a static file and Nest reading an upload are both read system calls
- a path traversal is a file-system bug in our code: a user-supplied name that contains `..` and escapes the upload folder. we join paths inside a root and reject the rest

- homework of chapter 5
```text
// 5a  what an inode stores that the filename does not
// 5b  name four system calls
// 5c  why deleting a file that a process still has open does not always free the disk yet
```

## chapter 6 The OSI model, TCP, and UDP

- OSI is a teaching stack of seven layers. real networks are talked about with four or five
- the layers we use: link (Ethernet, Wi-Fi), internet (IP), transport (TCP or UDP), application (HTTP, DNS)
- TCP = a stream that is reliable and ordered. lost packets are resent. HTTP lives on TCP
- UDP = a datagram. no connection, no retry inside the protocol. DNS queries and some video use it
- a TCP connection starts with a handshake. SYN, SYN-ACK, ACK. three packets before data
- closing is FIN in each direction
- a port = a number on one IP. 443 is HTTPS. our Nest process listens on one port behind nginx
- a socket = one end of a connection. the pair is local ip, local port, remote ip, remote port

```text
client SYN      -> server
client          <- SYN-ACK
client ACK      -> server
then HTTP bytes
```

- TLS sits on top of that handshake. the picture's TLS handshake is the next chapter
- UDP would not resend a lost laytime update. we use TCP, then HTTP or a WebSocket, which is TCP

- homework of chapter 6
```text
// 6a  TCP or UDP for an HTTP POST
// 6b  the three packets before the first HTTP byte
// 6c  what a port adds that an IP address does not
```

## chapter 7 IP, subnets, and DNS

- an IP address names a machine on a network. IPv4 looks like 203.0.113.10
- a subnet = a group of addresses that share a prefix
- 203.0.113.0/24 means the first 24 bits are the network. 256 addresses, of which the usual usable range is smaller
- a private range is not routed on the public internet. 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
- 127.0.0.1 is this machine. inside Docker, localhost is the container, not the laptop and not Postgres
- DNS = a name becomes an address. vms.arrobin.com becomes an IP
- the lookup is a query, often UDP, to a resolver, which may ask the authoritative server
- a record types we meet: A is an IPv4 address. CNAME is another name. AAAA is IPv6
- TTL on the record is how long a resolver may cache it

```text
vms.arrobin.com.   300  IN  A  203.0.113.10
```

- change the server, and old resolvers keep the old IP until the TTL ends
- a security group or a firewall is not DNS. DNS says where. the firewall says who may connect to the port

- homework of chapter 7
```text
// 7a  how many addresses in a /24, roughly
// 7b  why localhost inside the API container is not Postgres
// 7c  A record versus CNAME
// 7d  we change the A record and some users still hit the old box. what number explains the delay
```

## chapter 8 HTTP versions and TLS

- HTTP/1.1 = one request at a time on a connection, unless we pipeline, which clients mostly do not
- many files means many connections, or head-of-line blocking on one connection
- HTTP/2 = many streams on one connection. binary frames. header compression
- the browser still speaks HTTP/2 to nginx. nginx may speak HTTP/1.1 to Node. that is normal
- TLS = the bytes on the path are private, and the client checks the server name
- the handshake agrees a key. the certificate must match the domain, be in date, and chain to a trusted root
- HTTPS is HTTP inside TLS
- redirect HTTP to HTTPS
- TLS does not make a weak password strong, and it does not replace the role check
- on the public hop, TLS ends at nginx. nginx to Node on localhost can be plain HTTP

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- a certificate we never renew breaks the site on a Saturday
- HTTP/2 does not remove the need for small responses. it removes the need for a pile of connections

- homework of chapter 8
```text
// 8a  what HTTP/2 multiplexes
// 8b  three checks on a certificate
// 8c  is HTTP between nginx and Node on the same machine the public hop
```

## chapter 9 Sockets

- a socket is the API for a network connection
- the server binds a port and listens
- the client connects
- accept returns a new socket for that one client. the listen socket stays open for the next client
- we read and write bytes. HTTP is a protocol on top of those bytes
- WebSocket starts as HTTP and then switches protocols. it is still a socket
- our code uses Nest and Socket.IO. the operating system still has the listen socket

```ts
import net from "node:net";

const server = net.createServer((socket) => {
  socket.on("data", (buf) => {
    socket.write(`you said ${buf.toString()}`);
  });
});

server.listen(4000);
```

- this is TCP with no HTTP. a browser cannot open it as a web page
- one listen, many accepted sockets. that is how one port serves many users
- backpressure = the other side is slow. the socket buffer fills. we pause reading until drain

- homework of chapter 9
```ts
// 9a  which socket accepts the next client, the listen socket or the one accept returned
// 9b  why the snippet above is not an HTTP server
// 9c  what Socket.IO is sitting on
```

## chapter 10 Compilers, interpreters, garbage collection, and encoding

- a compiler translates source to another form before it runs. TypeScript compiles to JavaScript. that step erases the types
- an interpreter runs the source, or the bytecode, as it goes. the JavaScript engine does both: it parses, it may interpret, it may compile hot functions to machine code
- a garbage collector frees objects no one can reach
- we do not free objects by hand in JavaScript
- a mark-and-sweep collector marks objects reachable from roots, then sweeps the rest
- a global cache that still points at old responses keeps them alive. the collector is not a leak detector for "we forgot to delete the key"
- encoding = which bytes mean which character
- UTF-8 is the encoding on the web. ASCII is a subset. one byte for English letters, more bytes for other characters
- a string length in characters is not the byte length. a database column and a file size count bytes
- mojibake = bytes read as the wrong encoding

```ts
const text = "রউফ";
Buffer.byteLength(text, "utf8"); // more than text.length
```

- JSON is Unicode text. we send UTF-8
- a source file saved as UTF-8 and a database set to UTF-8 agree. a mix is how names break

- homework of chapter 10
```ts
// 10a  what the TypeScript compiler deletes
// 10b  why a Map that still holds a key is not collected
// 10c  why text.length and Buffer.byteLength can differ
```

## chapter 11 Scheduling a request through the stack

- one request, from the browser to the row, using the chapters above
- the browser resolves the name with DNS
- it opens TCP, then TLS, to nginx on 443
- nginx proxies to the Node process on a private port
- Node is one process, one JavaScript thread. the handler runs until it awaits Prisma
- during the await, the OS can schedule Postgres, and Node can start another request
- Prisma uses a pooled connection. the SQL is a transaction if we asked for one
- the response goes back through nginx

```text
browser
  DNS
  TCP + TLS
  nginx :443
  Node process
  pool
  Postgres
```

- a page fault or a full disk shows up as a slow read, then an error, not as a wrong status we invented
- two Node processes behind nginx do not share a lock in JavaScript. the lock that matters is in Postgres

- homework of chapter 11
```text
// 11a  list the hops for GET /port-calls/42
// 11b  where the JavaScript thread is free to take another request
// 11c  where the row lock lives
```

## chapter 12 Numbers we should be able to say

- these are the sizes and the names, so the chapters stay concrete
- a /24 is 256 addresses
- a common page is 4 KB
- TCP handshake is 3 packets
- HTTP/1.1 is one response at a time per connection. HTTP/2 has many streams
- localhost is 127.0.0.1, and inside a container it is that container
- UTF-8 is the encoding
- Postgres default isolation is read committed

```ts
function isPrivate(ip: string): boolean {
  return (
    ip.startsWith("10.") ||
    ip.startsWith("192.168.") ||
    ip.startsWith("127.")
  );
}
```

- 172.16.0.0/12 is also private. the function above is only the easy prefixes. 172.15 is not private. 172.16 through 172.31 are
- we use a library for real IP checks. the snippet is the idea

- homework of chapter 12
```text
// 12a  packets in a TCP handshake
// 12b  isolation level we get if we do not set one in Postgres
// 12c  encoding of a JSON API
// 12d  why 127.0.0.1 in the API container is the wrong host for Postgres
```
