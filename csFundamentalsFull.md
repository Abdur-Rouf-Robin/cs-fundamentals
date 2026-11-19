# CS Fundamentals

## Processes and threads

- A process is a running program with its own memory. A thread is a worker inside that process, sharing the memory.
- Node's JavaScript runs one main thread. The event loop interleaves callbacks. It does not run two JavaScript functions at the same instant on that thread.
- A second process, a PM2 worker or a BullMQ worker, has its own memory. They talk through Redis, HTTP, or the database.
- Threads inside one process share the heap, so they need locks. Processes do not share the heap.
- A crash of a thread can take the process. A crash of one process can leave the others up.
- A process is a house. Threads are people in the house who share the fridge. Two houses do not share a fridge.
- careful: Starting a hundred threads in your head and claiming Node does that for HTTP.
- PM2 and the separate queue worker are the process story you have lived.
- Is Node multithreaded?
- Your JavaScript is one thread per process. libuv uses a small thread pool for some blocking work such as bcrypt's underlying crypto and file IO. CPU-heavy JavaScript still blocks that process. I scale with more processes, which is what PM2 cluster does.

```
PM2 cluster: several Node processes
one process: one event loop, plus libuv's thread pool for some file and crypto work
```

- homework
```
PM2 cluster: several Node processes
one process: one event loop, plus libuv's thread pool for some file and crypto work
```

## Context switching

- A context switch is the CPU putting one task's registers aside and loading another's.
- The operating system saves the stack pointer and registers, then restores the next task.
- It costs time. Too many runnable threads means the CPU spends time switching instead of working.
- A switch into the kernel happens on a system call, a timer, or an interrupt.
- Your event loop avoids switches by not blocking. The cost moves to 'do not do heavy CPU work here'.
- It is changing desks: you pack your papers, the next person unpacks theirs. The packing is not free.
- careful: Thinking an async function creates a new CPU core. It does not.
- Why can fewer workers be faster?
- Past the number of cores, extra workers mostly wait and switch. I start near the core count, then measure. I do not set PM2 instances to 50 on a 4-core box.

```
one slow JSON loop on the main thread
=> every other request on that process waits
=> no context switch required for the damage
```

- homework
```
one slow JSON loop on the main thread
=> every other request on that process waits
=> no context switch required for the damage
```

## CPU scheduling

- The scheduler decides which ready task runs on a core.
- A task is ready, running, or blocked on I/O.
- Round robin gives each task a time slice, then moves it to the back.
- A priority scheduler can starve a low task unless there is ageing.
- For a web API, the scheduler you control is simpler: do not block, and run about one Node process per core.
- The scheduler is a referee with a whistle and a short turn for each player.
- careful: A tight while loop 'just to wait'. That is a running task that will not yield. Use a timer or I/O.
- What is starvation?
- A low-priority task that never runs because higher tasks keep arriving. Ageing raises its priority the longer it waits. In a queue, a job with no retry limit and a flood of new jobs is the same shape.

```
4 cores, 4 API workers, 1 queue worker
the OS schedules them
you keep each worker's JavaScript short
```

- homework
```
4 cores, 4 API workers, 1 queue worker
the OS schedules them
you keep each worker's JavaScript short
```

## Concurrency and locks

- Concurrency means the work overlaps in time. A lock makes a critical section run one at a time.
- Two workers incrementing one Redis key need a single atomic command, INCR, not get-then-set.
- A database row lock, SELECT FOR UPDATE, is the lock for a berth.
- A lock has an owner and a timeout, or a crashed worker holds it forever.
- Prefer a unique constraint over a lock when the rule is 'this id exists once'.
- A lock is the bathroom sign. Atomic is better when the database can do the whole step in one move.
- careful: get, check, set, with no atomic command and no transaction.
- Redis INCR for rate limits is the atomic example you have.
- What is a race?
- Two workers both read berth free, both write booked. The second write wins and two ships think they have it. The fix is one atomic update: UPDATE berths SET ship = $1 WHERE id = $2 AND ship IS NULL, and check that one row changed.

```
await redis.set(`lock:${id}`, token, "NX", "PX", 5000);
```

- homework
```
await redis.set(`lock:${id}`, token, "NX", "PX", 5000);
```

## Deadlocks

- A deadlock is a circle of waits. Each holder wants something the next one holds.
- Transaction A locks row 1 and wants row 2. Transaction B locks row 2 and wants row 1.
- Prevention: always lock rows in the same order, such as by id.
- Postgres detects a deadlock and aborts one transaction. You retry it.
- A lock timeout is the other escape. Waiting forever is not a strategy.
- Two people in a corridor, each waiting for the other to step back. Someone has to be told to start again.
- careful: Catching the error and retrying instantly in a tight loop with no limit.
- How do you see it?
- One request hangs, the database shows two sessions waiting on each other. The application log shows a deadlock error on one of them. I make the lock order the same in every code path.

```
always lock berths in order of id
retry the transaction that Postgres aborts
```

- homework
```
always lock berths in order of id
retry the transaction that Postgres aborts
```

## Memory management

- The process gets virtual memory. The allocator hands out pieces of the heap. Garbage collection in JavaScript frees what no variable can reach.
- The stack holds the current function's locals and returns when the function returns.
- The heap holds objects that outlive the function. Closures keep a heap object alive.
- A leak is an object you no longer need that a global, a cache, or a socket map still points at.
- A Buffer of a video is large. Do not hold every upload in an array 'just in case'.
- Memory is a desk. The stack is the paper in your hand. The heap is the drawers. A leak is a drawer you keep filling and never empty.
- careful: An unbounded in-memory cache in front of Postgres.
- What do you look at when Node memory climbs?
- A map that grows with every request, a socket that never leaves its room, or a queue of buffers. I take a heap snapshot if the graph does not plateau. A cache without a max size is the usual bug.

```typescript
const cache = new Map(); // if you never delete, this is a leak
```

- homework
```typescript
const cache = new Map(); // if you never delete, this is a leak
```

## Virtual memory and paging

- Every process believes it has a private address space. The CPU and the OS map those addresses to real RAM in pages.
- A page is a fixed block, often 4 KB.
- A page table maps virtual pages to physical frames.
- If the page is not in RAM, a page fault loads it from disk. Too many faults is thrashing, and the machine gets slow while the CPU looks idle.
- Two processes cannot read each other's virtual addresses. That is why one Node crash does not expose another's heap, and also why they cannot share an object by pointer.
- Virtual memory is a library index. The book may be on the shelf or in the basement. You use the same call number either way.
- careful: Adding RAM in your head as the fix for a leak. The leak will fill the new RAM too.
- Why does a 16 GB Node heap not mean 16 GB of RAM is reserved?
- The address space is virtual. Pages are backed when you touch them. Asking the OS for address space is not the same as filling RAM.

```
virtual page -> page table -> RAM frame, or a fault to disk
```

- homework
```
virtual page -> page table -> RAM frame, or a fault to disk
```

## File systems

- A file system names bytes on disk and controls who may read them.
- A path is directories plus a name. The inode is the record of size, owner, and where the blocks live.
- Permissions are read, write, execute, for owner, group, and others.
- A delete removes a name. The bytes go away when the last name and the last open handle are gone.
- Do not serve user uploads from the directory that holds your source. Put them in object storage or a folder the app cannot execute.
- The path is the label on the drawer. The inode is the drawer itself. Two labels can point at one drawer, which is a hard link.
- careful: chmod 777 because a write failed.
- Why can a deleted log file still fill the disk?
- A process still has it open. The name is gone, the inode remains until PM2 restarts or the process closes the handle. I check open deleted files before I blame the new deploy.

```bash
ls -l upload.mp4
chmod 640 upload.mp4
```

- homework
```bash
ls -l upload.mp4
chmod 640 upload.mp4
```

## System calls

- A system call is the programme asking the kernel to do something it is not allowed to do alone.
- read, write, open, close, and socket calls are system calls.
- Crossing into the kernel has a cost. A loop of one-byte reads is slower than a buffered read.
- Your JavaScript fs.readFile ends in a system call on the libuv pool.
- You almost never write the syscall. You should know that the OS, not V8, owns the disk and the network.
- A system call is the counter at a bank. You do not walk into the vault. You pass a slip.
- careful: Thinking fs promises skip the operating system.
- What is the kernel for, in one line?
- It is the only part that may talk to the hardware and isolate processes. Everything else asks it.

```
open, read, write, close, accept, epoll/kqueue
```

- homework
```
open, read, write, close, accept, epoll/kqueue
```

## OSI model

- The OSI model is seven names for layers of a network. You use it to say where a bug lives.
- Physical and data link: cables, Wi-Fi, MAC addresses.
- Network: IP addresses and routing.
- Transport: TCP and UDP, ports.
- Application: HTTP, DNS, TLS sits between application and transport in the way people draw it now.
- If ping works and HTTP does not, the network layer is alive and the application or the port is the problem.
- It is a stack of envelopes. Each desk adds one envelope and does not read the letter inside.
- careful: Memorising seven names and being unable to say whether the failure is DNS, TCP, or HTTP.
- Which layer is a 502?
- Your proxy, nginx, spoke HTTP and the upstream did not answer properly. The cables are fine. The application process or the upstream timeout is the layer to open.

```
ping: ICMP, network layer
curl: HTTP over TCP, and TLS if it is https
```

- homework
```
ping: ICMP, network layer
curl: HTTP over TCP, and TLS if it is https
```

## TCP vs UDP

- TCP is a reliable, ordered stream. UDP is a short message with no promise.
- TCP handshakes, numbers the bytes, retransmits loss, and slows down when the network is full.
- UDP sends a datagram. If it vanishes, the sender is not told, unless the application builds that.
- HTTP, Postgres, and SSH use TCP.
- A live game position or a video packet sometimes uses UDP because a late packet is useless. HLS over HTTP is TCP, which is what Anemi uses.
- TCP is a signed-for parcel. UDP is a postcard. The postcard is faster and may never arrive.
- careful: Saying WebSockets are UDP. They are TCP.
- Why is video over TCP all right for Anemi?
- HLS can buffer a few seconds. A retransmit is cheaper than a glitch in a film. A real-time call cannot wait, and that is where UDP shows up. I do not pretend Anemi is UDP.

```
TCP: web, API, Postgres
UDP: DNS queries, some voice
Anemi: HTTP, so TCP
```

- homework
```
TCP: web, API, Postgres
UDP: DNS queries, some voice
Anemi: HTTP, so TCP
```

## TCP handshake

- TCP starts with three packets so both sides know the other can send and receive.
- The client sends SYN, with a sequence number.
- The server replies SYN-ACK, with its own number and an acknowledgement.
- The client sends ACK. The connection is established. Then TLS can start, then HTTP.
- A SYN flood sends SYNs and never finishes. The server's half-open table fills. SYN cookies and a proxy are the defence, not an application if-statement.
- SYN is a raised hand. SYN-ACK is 'I see you, here is my hand'. ACK is 'I see yours'. Then you talk.
- careful: Drawing TLS before TCP.
- Where does HTTPS sit?
- After the TCP handshake. TLS is the next conversation on that connection. Then HTTP. Three steps, in that order.

```
client SYN -> server
server SYN-ACK -> client
client ACK -> server
```

- homework
```
client SYN -> server
server SYN-ACK -> client
client ACK -> server
```

## IP and subnets

- An IP address locates a machine on a network. A subnet is the slice of addresses that share a prefix.
- IPv4 is four bytes. 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private.
- The /24 in 192.168.1.0/24 means the first 24 bits are the network. The last 8 bits are hosts, 256 addresses, minus network and broadcast.
- A gateway is the router that forwards packets leaving the subnet.
- Docker gives containers addresses on a bridge network. The host's localhost is not the container's localhost.
- A subnet is a street. The /24 is how long the street name is. The gateway is the junction to other streets.
- careful: Pointing DATABASE_URL at localhost inside a container.
- Your Compose file is the example.
- Why does the API in Compose call the database db and not localhost?
- localhost inside the API container is the API container. The database is a different container. Compose DNS name db resolves on the compose network.

```
192.168.1.20/24
network 192.168.1.0
usable .1 to .254
gateway often .1
```

- homework
```
192.168.1.20/24
network 192.168.1.0
usable .1 to .254
gateway often .1
```

## DNS

- DNS turns a name into an address.
- The browser asks a resolver. The resolver asks the root, then the TLD, then the authoritative server, unless a cache already knows.
- An A record is an IPv4 address. A CNAME is an alias to another name.
- TTL is how long a cache may remember. A long TTL makes a migration slow to be seen.
- A failure here looks like a site that is 'down' while the server is healthy. Check the name before you restart Node.
- DNS is the phone book. The TTL is how long someone may keep an old photocopy of the page.
- careful: Restarting the API because a name does not resolve.
- Your three domains are the story.
- You changed the server IP and some users still see the old site. Why?
- Their resolver, or the browser, is inside the TTL. I lower the TTL before a move, and I wait out the old TTL.

```
anime.arrobin.com -> A or CNAME -> address -> TCP -> TLS -> HTTP
```

- homework
```
anime.arrobin.com -> A or CNAME -> address -> TCP -> TLS -> HTTP
```

## HTTP/1.1 vs HTTP/2

- HTTP/1.1 speaks text and often needs several connections. HTTP/2 speaks binary frames and multiplexes many streams on one connection.
- HTTP/1.1 pipelining was awkward. Browsers opened many connections instead.
- HTTP/2 lets many requests share one TCP connection without blocking each other at the HTTP layer.
- Head-of-line blocking still exists at TCP: one lost packet stalls every stream on that connection. HTTP/3 moves to QUIC over UDP to ease that.
- Server push exists in HTTP/2 and is rarely what you want. Do not lead with it.
- HTTP/1.1 is several phone calls. HTTP/2 is one call where you can talk about several topics without hanging up.
- careful: Blaming HTTP version for a missing index.
- Does HTTP/2 make a slow SQL query fast?
- No. It removes connection overhead. The query is still the query. I do not 'turn on HTTP/2' as the fix for a slow port-call page.

```
HTTP/1.1: several TCP connections
HTTP/2: one connection, many streams
```

- homework
```
HTTP/1.1: several TCP connections
HTTP/2: one connection, many streams
```

## TLS handshake

- TLS agrees a shared secret and checks the server's certificate, on top of TCP.
- The client says which versions and ciphers it can use.
- The server sends its certificate. The client checks the name, the dates, and the chain up to a trusted root.
- They agree a session key. Modern TLS uses an ephemeral key so a later stolen server key cannot decrypt today's traffic.
- Then HTTP is encrypted. The certificate does not mean the application is safe. It means you are talking to the name you asked for, if the check passed.
- TLS is sealing the envelope and checking the letterhead. It is not a review of the letter.
- careful: A certificate for the wrong name, or a clock so wrong the dates fail.
- nginx or Caddy terminates TLS in front of Nest.
- What does HTTPS guarantee?
- That the bytes were not altered on the path, and that the certificate matches the name, if the client checked it. It does not guarantee that my code is correct or that I stored the password well.

```
TCP, then TLS, then HTTP
certificate name must match anime.arrobin.com
```

- homework
```
TCP, then TLS, then HTTP
certificate name must match anime.arrobin.com
```

## Sockets

- A socket is one end of a connection: an address, a port, and a protocol.
- A server socket listens. accept gives a new socket per client.
- A port is a number on that machine. 443 is HTTPS. Your API might be 3000 behind nginx.
- One process can hold many sockets. The event loop waits on them.
- CLOSE_WAIT and a pile of open sockets means something is not closing connections, often a client that disappeared or a keep-alive you never idle out.
- A socket is a phone line. The port is the extension. nginx answers the public extension and transfers the call to Nest.
- careful: Binding the API on a public port and also on nginx, with no firewall, so people skip the proxy.
- Why can only one process listen on a port?
- One listener owns the port, unless you use the kernel's shared listen, which Node cluster does so several workers can accept. Two unrelated programmes cannot both bind 3000.

```
nginx :443 -> proxy_pass 127.0.0.1:3000
```

- homework
```
nginx :443 -> proxy_pass 127.0.0.1:3000
```

## Compilers vs interpreters

- A compiler translates the programme ahead of time. An interpreter executes it as it goes. JavaScript is compiled just in time inside V8, which is both stories.
- TypeScript is type-checked and then erased to JavaScript. tsc or your bundler does that. There is no TypeScript runtime.
- V8 parses JavaScript and JIT-compiles hot functions to machine code.
- A Go or Rust binary is compiled ahead of time. You ship the machine code.
- The practical point: a type error fails the build. A logic error still ships.
- A compiler is translating the whole book before opening night. A JIT is translating the scenes the audience actually watches, during the show.
- careful: Saying TypeScript 'runs' on the server. JavaScript runs. The types are gone.
- Why did a type error not save production?
- The bug was a wrong business rule, and the types were happy. Or the bad value came from JSON and was typed as any. Types are a build-time net, not a test of laytime.

```
.ts  --tsc/bundler-->  .js  --V8 JIT-->  machine code
```

- homework
```
.ts  --tsc/bundler-->  .js  --V8 JIT-->  machine code
```

## Garbage collection

- V8 reclaims objects that no root can reach. A root is a global, a stack local, or another live object.
- A minor collection cleans the nursery, where young objects die fast.
- A major collection walks older objects. It pauses more.
- A closure, a global cache, or a timer that still points at a big object keeps it alive.
- You do not call free. You drop the reference.
- The collector is a janitor who may only throw away a box nobody's hand is on.
- careful: Deleting a property and thinking a large graph is gone while an array still holds it.
- The heap grows and then falls in a saw. Is that a leak?
- Not by itself. Allocation and collection look like a saw. A leak is a saw whose low point keeps rising after each collection. I look at the floor, not the spikes.

```typescript
let buf: Buffer | null = await fs.readFile(path);
buf = null; // the buffer can be collected after this, if nothing else points at it
```

- homework
```typescript
let buf: Buffer | null = await fs.readFile(path);
buf = null; // the buffer can be collected after this, if nothing else points at it
```

## Character encoding

- An encoding is the agreement on which bytes mean which character.
- ASCII is the old English set. UTF-8 is the web's Unicode encoding. It is one byte for English and more bytes for Bangla.
- A string in JavaScript is UTF-16 code units. A Buffer is bytes. Converting with the wrong encoding mojibake's the name.
- The database, the HTTP header, and the file must agree. Postgres can store UTF-8. Set the client encoding and the HTML charset.
- Emoji and some Bangla characters are more than one code unit. Do not slice a string on byte length and assume you cut a character.
- Encoding is the alphabet you agreed to write in. If one person uses another alphabet, the letters are not wrong. The agreement is.
- careful: Slicing a UTF-16 string in the middle of a character, or treating string length as the byte size of a JWT.
- Your CV carries a Bangla name. This question is personal, not abstract.
- Why did a name turn into question marks?
- Some step decoded UTF-8 bytes as Latin-1, or the column was not UTF-8, or a CSV was saved as a different encoding. I name the boundary that converted the bytes.

```typescript
Buffer.from("মোঃ আব্দুর রউফ", "utf8")
```

- homework
```typescript
Buffer.from("মোঃ আব্দুর রউফ", "utf8")
```
