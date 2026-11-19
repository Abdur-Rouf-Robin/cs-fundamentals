# CS Fundamentals

Study notes for this card. Same shape as the JavaScript notes: a fact, the mechanism, code you can type, a spoken answer, then homework.

Read one concept out loud. Close the file. Type the example. Answer the question without looking.

A line the play button covered on the photo is filled in here as the usual concept for that number.

## 01 Processes and threads

- A process is a running program with its own memory. A thread is a worker inside that process, sharing the memory.

- Node's JavaScript runs one main thread. The event loop interleaves callbacks. It does not run two JavaScript functions at the same instant on that thread.
- A second process, a PM2 worker or a BullMQ worker, has its own memory. They talk through Redis, HTTP, or the database.
- Threads inside one process share the heap, so they need locks. Processes do not share the heap.
- A crash of a thread can take the process. A crash of one process can leave the others up.

```
PM2 cluster: several Node processes
one process: one event loop, plus libuv's thread pool for some file and crypto work
```

Question. Is Node multithreaded?

Say this. Your JavaScript is one thread per process. libuv uses a small thread pool for some blocking work such as bcrypt's underlying crypto and file IO. CPU-heavy JavaScript still blocks that process. I scale with more processes, which is what PM2 cluster does.

Teach it. A process is a house. Threads are people in the house who share the fridge. Two houses do not share a fridge.

The mistake. Starting a hundred threads in your head and claiming Node does that for HTTP.

On your CV. PM2 and the separate queue worker are the process story you have lived.

### homework

- Close the page and answer out loud: Is Node multithreaded?

## 02 Context switching

- A context switch is the CPU putting one task's registers aside and loading another's.

- The operating system saves the stack pointer and registers, then restores the next task.
- It costs time. Too many runnable threads means the CPU spends time switching instead of working.
- A switch into the kernel happens on a system call, a timer, or an interrupt.
- Your event loop avoids switches by not blocking. The cost moves to 'do not do heavy CPU work here'.

```
one slow JSON loop on the main thread
=> every other request on that process waits
=> no context switch required for the damage
```

Question. Why can fewer workers be faster?

Say this. Past the number of cores, extra workers mostly wait and switch. I start near the core count, then measure. I do not set PM2 instances to 50 on a 4-core box.

Teach it. It is changing desks: you pack your papers, the next person unpacks theirs. The packing is not free.

The mistake. Thinking an async function creates a new CPU core. It does not.

### homework

- Close the page and answer out loud: Why can fewer workers be faster?

## 03 CPU scheduling

- The scheduler decides which ready task runs on a core.

- A task is ready, running, or blocked on I/O.
- Round robin gives each task a time slice, then moves it to the back.
- A priority scheduler can starve a low task unless there is ageing.
- For a web API, the scheduler you control is simpler: do not block, and run about one Node process per core.

```
4 cores, 4 API workers, 1 queue worker
the OS schedules them
you keep each worker's JavaScript short
```

Question. What is starvation?

Say this. A low-priority task that never runs because higher tasks keep arriving. Ageing raises its priority the longer it waits. In a queue, a job with no retry limit and a flood of new jobs is the same shape.

Teach it. The scheduler is a referee with a whistle and a short turn for each player.

The mistake. A tight while loop 'just to wait'. That is a running task that will not yield. Use a timer or I/O.

### homework

- Close the page and answer out loud: What is starvation?

## 04 Concurrency and locks

- Concurrency means the work overlaps in time. A lock makes a critical section run one at a time.

- Two workers incrementing one Redis key need a single atomic command, INCR, not get-then-set.
- A database row lock, SELECT FOR UPDATE, is the lock for a berth.
- A lock has an owner and a timeout, or a crashed worker holds it forever.
- Prefer a unique constraint over a lock when the rule is 'this id exists once'.

```
await redis.set(`lock:${id}`, token, "NX", "PX", 5000);
```

Question. What is a race?

Say this. Two workers both read berth free, both write booked. The second write wins and two ships think they have it. The fix is one atomic update: UPDATE berths SET ship = $1 WHERE id = $2 AND ship IS NULL, and check that one row changed.

Teach it. A lock is the bathroom sign. Atomic is better when the database can do the whole step in one move.

The mistake. get, check, set, with no atomic command and no transaction.

On your CV. Redis INCR for rate limits is the atomic example you have.

### homework

- Close the page and answer out loud: What is a race?

## 05 Deadlocks

- A deadlock is a circle of waits. Each holder wants something the next one holds.

- Transaction A locks row 1 and wants row 2. Transaction B locks row 2 and wants row 1.
- Prevention: always lock rows in the same order, such as by id.
- Postgres detects a deadlock and aborts one transaction. You retry it.
- A lock timeout is the other escape. Waiting forever is not a strategy.

```
always lock berths in order of id
retry the transaction that Postgres aborts
```

Question. How do you see it?

Say this. One request hangs, the database shows two sessions waiting on each other. The application log shows a deadlock error on one of them. I make the lock order the same in every code path.

Teach it. Two people in a corridor, each waiting for the other to step back. Someone has to be told to start again.

The mistake. Catching the error and retrying instantly in a tight loop with no limit.

### homework

- Close the page and answer out loud: How do you see it?

## 06 Memory management

- The process gets virtual memory. The allocator hands out pieces of the heap. Garbage collection in JavaScript frees what no variable can reach.

- The stack holds the current function's locals and returns when the function returns.
- The heap holds objects that outlive the function. Closures keep a heap object alive.
- A leak is an object you no longer need that a global, a cache, or a socket map still points at.
- A Buffer of a video is large. Do not hold every upload in an array 'just in case'.

```typescript
const cache = new Map(); // if you never delete, this is a leak
```

Question. What do you look at when Node memory climbs?

Say this. A map that grows with every request, a socket that never leaves its room, or a queue of buffers. I take a heap snapshot if the graph does not plateau. A cache without a max size is the usual bug.

Teach it. Memory is a desk. The stack is the paper in your hand. The heap is the drawers. A leak is a drawer you keep filling and never empty.

The mistake. An unbounded in-memory cache in front of Postgres.

### homework

- Close the page and answer out loud: What do you look at when Node memory climbs?

## 07 Virtual memory and paging

- Every process believes it has a private address space. The CPU and the OS map those addresses to real RAM in pages.

- A page is a fixed block, often 4 KB.
- A page table maps virtual pages to physical frames.
- If the page is not in RAM, a page fault loads it from disk. Too many faults is thrashing, and the machine gets slow while the CPU looks idle.
- Two processes cannot read each other's virtual addresses. That is why one Node crash does not expose another's heap, and also why they cannot share an object by pointer.

```
virtual page -> page table -> RAM frame, or a fault to disk
```

Question. Why does a 16 GB Node heap not mean 16 GB of RAM is reserved?

Say this. The address space is virtual. Pages are backed when you touch them. Asking the OS for address space is not the same as filling RAM.

Teach it. Virtual memory is a library index. The book may be on the shelf or in the basement. You use the same call number either way.

The mistake. Adding RAM in your head as the fix for a leak. The leak will fill the new RAM too.

### homework

- Close the page and answer out loud: Why does a 16 GB Node heap not mean 16 GB of RAM is reserved?

## 08 File systems

- A file system names bytes on disk and controls who may read them.

- A path is directories plus a name. The inode is the record of size, owner, and where the blocks live.
- Permissions are read, write, execute, for owner, group, and others.
- A delete removes a name. The bytes go away when the last name and the last open handle are gone.
- Do not serve user uploads from the directory that holds your source. Put them in object storage or a folder the app cannot execute.

```bash
ls -l upload.mp4
chmod 640 upload.mp4
```

Question. Why can a deleted log file still fill the disk?

Say this. A process still has it open. The name is gone, the inode remains until PM2 restarts or the process closes the handle. I check open deleted files before I blame the new deploy.

Teach it. The path is the label on the drawer. The inode is the drawer itself. Two labels can point at one drawer, which is a hard link.

The mistake. chmod 777 because a write failed.

### homework

- Close the page and answer out loud: Why can a deleted log file still fill the disk?

## 09 System calls

- A system call is the programme asking the kernel to do something it is not allowed to do alone.

- read, write, open, close, and socket calls are system calls.
- Crossing into the kernel has a cost. A loop of one-byte reads is slower than a buffered read.
- Your JavaScript fs.readFile ends in a system call on the libuv pool.
- You almost never write the syscall. You should know that the OS, not V8, owns the disk and the network.

```
open, read, write, close, accept, epoll/kqueue
```

Question. What is the kernel for, in one line?

Say this. It is the only part that may talk to the hardware and isolate processes. Everything else asks it.

Teach it. A system call is the counter at a bank. You do not walk into the vault. You pass a slip.

The mistake. Thinking fs promises skip the operating system.

### homework

- Close the page and answer out loud: What is the kernel for, in one line?

## 10 OSI model

- The OSI model is seven names for layers of a network. You use it to say where a bug lives.

- Physical and data link: cables, Wi-Fi, MAC addresses.
- Network: IP addresses and routing.
- Transport: TCP and UDP, ports.
- Application: HTTP, DNS, TLS sits between application and transport in the way people draw it now.
- If ping works and HTTP does not, the network layer is alive and the application or the port is the problem.

```
ping: ICMP, network layer
curl: HTTP over TCP, and TLS if it is https
```

Question. Which layer is a 502?

Say this. Your proxy, nginx, spoke HTTP and the upstream did not answer properly. The cables are fine. The application process or the upstream timeout is the layer to open.

Teach it. It is a stack of envelopes. Each desk adds one envelope and does not read the letter inside.

The mistake. Memorising seven names and being unable to say whether the failure is DNS, TCP, or HTTP.

### homework

- Close the page and answer out loud: Which layer is a 502?

## 11 TCP vs UDP

- TCP is a reliable, ordered stream. UDP is a short message with no promise.

- TCP handshakes, numbers the bytes, retransmits loss, and slows down when the network is full.
- UDP sends a datagram. If it vanishes, the sender is not told, unless the application builds that.
- HTTP, Postgres, and SSH use TCP.
- A live game position or a video packet sometimes uses UDP because a late packet is useless. HLS over HTTP is TCP, which is what Anemi uses.

```
TCP: web, API, Postgres
UDP: DNS queries, some voice
Anemi: HTTP, so TCP
```

Question. Why is video over TCP all right for Anemi?

Say this. HLS can buffer a few seconds. A retransmit is cheaper than a glitch in a film. A real-time call cannot wait, and that is where UDP shows up. I do not pretend Anemi is UDP.

Teach it. TCP is a signed-for parcel. UDP is a postcard. The postcard is faster and may never arrive.

The mistake. Saying WebSockets are UDP. They are TCP.

### homework

- Close the page and answer out loud: Why is video over TCP all right for Anemi?

## 12 TCP handshake

- TCP starts with three packets so both sides know the other can send and receive.

- The client sends SYN, with a sequence number.
- The server replies SYN-ACK, with its own number and an acknowledgement.
- The client sends ACK. The connection is established. Then TLS can start, then HTTP.
- A SYN flood sends SYNs and never finishes. The server's half-open table fills. SYN cookies and a proxy are the defence, not an application if-statement.

```
client SYN -> server
server SYN-ACK -> client
client ACK -> server
```

Question. Where does HTTPS sit?

Say this. After the TCP handshake. TLS is the next conversation on that connection. Then HTTP. Three steps, in that order.

Teach it. SYN is a raised hand. SYN-ACK is 'I see you, here is my hand'. ACK is 'I see yours'. Then you talk.

The mistake. Drawing TLS before TCP.

### homework

- Close the page and answer out loud: Where does HTTPS sit?

## 13 IP and subnets

- An IP address locates a machine on a network. A subnet is the slice of addresses that share a prefix.

- IPv4 is four bytes. 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private.
- The /24 in 192.168.1.0/24 means the first 24 bits are the network. The last 8 bits are hosts, 256 addresses, minus network and broadcast.
- A gateway is the router that forwards packets leaving the subnet.
- Docker gives containers addresses on a bridge network. The host's localhost is not the container's localhost.

```
192.168.1.20/24
network 192.168.1.0
usable .1 to .254
gateway often .1
```

Question. Why does the API in Compose call the database db and not localhost?

Say this. localhost inside the API container is the API container. The database is a different container. Compose DNS name db resolves on the compose network.

Teach it. A subnet is a street. The /24 is how long the street name is. The gateway is the junction to other streets.

The mistake. Pointing DATABASE_URL at localhost inside a container.

On your CV. Your Compose file is the example.

### homework

- Close the page and answer out loud: Why does the API in Compose call the database db and not localhost?

## 14 DNS

- DNS turns a name into an address.

- The browser asks a resolver. The resolver asks the root, then the TLD, then the authoritative server, unless a cache already knows.
- An A record is an IPv4 address. A CNAME is an alias to another name.
- TTL is how long a cache may remember. A long TTL makes a migration slow to be seen.
- A failure here looks like a site that is 'down' while the server is healthy. Check the name before you restart Node.

```
anime.arrobin.com -> A or CNAME -> address -> TCP -> TLS -> HTTP
```

Question. You changed the server IP and some users still see the old site. Why?

Say this. Their resolver, or the browser, is inside the TTL. I lower the TTL before a move, and I wait out the old TTL.

Teach it. DNS is the phone book. The TTL is how long someone may keep an old photocopy of the page.

The mistake. Restarting the API because a name does not resolve.

On your CV. Your three domains are the story.

### homework

- Close the page and answer out loud: You changed the server IP and some users still see the old site. Why?

## 15 HTTP/1.1 vs HTTP/2

- HTTP/1.1 speaks text and often needs several connections. HTTP/2 speaks binary frames and multiplexes many streams on one connection.

- HTTP/1.1 pipelining was awkward. Browsers opened many connections instead.
- HTTP/2 lets many requests share one TCP connection without blocking each other at the HTTP layer.
- Head-of-line blocking still exists at TCP: one lost packet stalls every stream on that connection. HTTP/3 moves to QUIC over UDP to ease that.
- Server push exists in HTTP/2 and is rarely what you want. Do not lead with it.

```
HTTP/1.1: several TCP connections
HTTP/2: one connection, many streams
```

Question. Does HTTP/2 make a slow SQL query fast?

Say this. No. It removes connection overhead. The query is still the query. I do not 'turn on HTTP/2' as the fix for a slow port-call page.

Teach it. HTTP/1.1 is several phone calls. HTTP/2 is one call where you can talk about several topics without hanging up.

The mistake. Blaming HTTP version for a missing index.

### homework

- Close the page and answer out loud: Does HTTP/2 make a slow SQL query fast?

## 16 TLS handshake

- TLS agrees a shared secret and checks the server's certificate, on top of TCP.

- The client says which versions and ciphers it can use.
- The server sends its certificate. The client checks the name, the dates, and the chain up to a trusted root.
- They agree a session key. Modern TLS uses an ephemeral key so a later stolen server key cannot decrypt today's traffic.
- Then HTTP is encrypted. The certificate does not mean the application is safe. It means you are talking to the name you asked for, if the check passed.

```
TCP, then TLS, then HTTP
certificate name must match anime.arrobin.com
```

Question. What does HTTPS guarantee?

Say this. That the bytes were not altered on the path, and that the certificate matches the name, if the client checked it. It does not guarantee that my code is correct or that I stored the password well.

Teach it. TLS is sealing the envelope and checking the letterhead. It is not a review of the letter.

The mistake. A certificate for the wrong name, or a clock so wrong the dates fail.

On your CV. nginx or Caddy terminates TLS in front of Nest.

### homework

- Close the page and answer out loud: What does HTTPS guarantee?

## 17 Sockets

- A socket is one end of a connection: an address, a port, and a protocol.

- A server socket listens. accept gives a new socket per client.
- A port is a number on that machine. 443 is HTTPS. Your API might be 3000 behind nginx.
- One process can hold many sockets. The event loop waits on them.
- CLOSE_WAIT and a pile of open sockets means something is not closing connections, often a client that disappeared or a keep-alive you never idle out.

```
nginx :443 -> proxy_pass 127.0.0.1:3000
```

Question. Why can only one process listen on a port?

Say this. One listener owns the port, unless you use the kernel's shared listen, which Node cluster does so several workers can accept. Two unrelated programmes cannot both bind 3000.

Teach it. A socket is a phone line. The port is the extension. nginx answers the public extension and transfers the call to Nest.

The mistake. Binding the API on a public port and also on nginx, with no firewall, so people skip the proxy.

### homework

- Close the page and answer out loud: Why can only one process listen on a port?

## 18 Compilers vs interpreters

- A compiler translates the programme ahead of time. An interpreter executes it as it goes. JavaScript is compiled just in time inside V8, which is both stories.

- TypeScript is type-checked and then erased to JavaScript. tsc or your bundler does that. There is no TypeScript runtime.
- V8 parses JavaScript and JIT-compiles hot functions to machine code.
- A Go or Rust binary is compiled ahead of time. You ship the machine code.
- The practical point: a type error fails the build. A logic error still ships.

```
.ts  --tsc/bundler-->  .js  --V8 JIT-->  machine code
```

Question. Why did a type error not save production?

Say this. The bug was a wrong business rule, and the types were happy. Or the bad value came from JSON and was typed as any. Types are a build-time net, not a test of laytime.

Teach it. A compiler is translating the whole book before opening night. A JIT is translating the scenes the audience actually watches, during the show.

The mistake. Saying TypeScript 'runs' on the server. JavaScript runs. The types are gone.

### homework

- Close the page and answer out loud: Why did a type error not save production?

## 19 Garbage collection

- V8 reclaims objects that no root can reach. A root is a global, a stack local, or another live object.

- A minor collection cleans the nursery, where young objects die fast.
- A major collection walks older objects. It pauses more.
- A closure, a global cache, or a timer that still points at a big object keeps it alive.
- You do not call free. You drop the reference.

```typescript
let buf: Buffer | null = await fs.readFile(path);
buf = null; // the buffer can be collected after this, if nothing else points at it
```

Question. The heap grows and then falls in a saw. Is that a leak?

Say this. Not by itself. Allocation and collection look like a saw. A leak is a saw whose low point keeps rising after each collection. I look at the floor, not the spikes.

Teach it. The collector is a janitor who may only throw away a box nobody's hand is on.

The mistake. Deleting a property and thinking a large graph is gone while an array still holds it.

### homework

- Close the page and answer out loud: The heap grows and then falls in a saw. Is that a leak?

## 20 Character encoding

- An encoding is the agreement on which bytes mean which character.

- ASCII is the old English set. UTF-8 is the web's Unicode encoding. It is one byte for English and more bytes for Bangla.
- A string in JavaScript is UTF-16 code units. A Buffer is bytes. Converting with the wrong encoding mojibake's the name.
- The database, the HTTP header, and the file must agree. Postgres can store UTF-8. Set the client encoding and the HTML charset.
- Emoji and some Bangla characters are more than one code unit. Do not slice a string on byte length and assume you cut a character.

```typescript
Buffer.from("মোঃ আব্দুর রউফ", "utf8")
```

Question. Why did a name turn into question marks?

Say this. Some step decoded UTF-8 bytes as Latin-1, or the column was not UTF-8, or a CSV was saved as a different encoding. I name the boundary that converted the bytes.

Teach it. Encoding is the alphabet you agreed to write in. If one person uses another alphabet, the letters are not wrong. The agreement is.

The mistake. Slicing a UTF-16 string in the middle of a character, or treating string length as the byte size of a JWT.

On your CV. Your CV carries a Bangla name. This question is personal, not abstract.

### homework

- Close the page and answer out loud: Why did a name turn into question marks?

## Homework for the whole file

1. Read the twenty titles out loud with the file closed.
2. Pick three and write the example from memory.
3. Teach one concept to an empty chair in under a minute.
