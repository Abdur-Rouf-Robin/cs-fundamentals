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

- example 1. process and thread while handling pc_12
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 72000; i++) n++;
// request pc_12 cannot finish other handlers until this loop returns
```

- homework
```ts
// 1a  pc_12 handled in process A is not in process B's heap
// 1b  two threads in one process can both see a shared array
// 1c  the for-loop is not an await. it does not yield
```

- example 2. process and thread while handling m_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 3000; i++) n++;
// request m_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 2a  m_1 handled in process A is not in process B's heap
// 2b  two threads in one process can both see a shared array
// 2c  the for-loop is not an await. it does not yield
```

- example 3. process and thread while handling t_9
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 16000; i++) n++;
// request t_9 cannot finish other handlers until this loop returns
```

- homework
```ts
// 3a  t_9 handled in process A is not in process B's heap
// 3b  two threads in one process can both see a shared array
// 3c  the for-loop is not an await. it does not yield
```

- example 4. process and thread while handling v_4
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 6000; i++) n++;
// request v_4 cannot finish other handlers until this loop returns
```

- homework
```ts
// 4a  v_4 handled in process A is not in process B's heap
// 4b  two threads in one process can both see a shared array
// 4c  the for-loop is not an await. it does not yield
```

- example 5. process and thread while handling f_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 1000; i++) n++;
// request f_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 5a  f_2 handled in process A is not in process B's heap
// 5b  two threads in one process can both see a shared array
// 5c  the for-loop is not an await. it does not yield
```

- example 6. process and thread while handling u_3
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 1000; i++) n++;
// request u_3 cannot finish other handlers until this loop returns
```

- homework
```ts
// 6a  u_3 handled in process A is not in process B's heap
// 6b  two threads in one process can both see a shared array
// 6c  the for-loop is not an await. it does not yield
```

- example 7. process and thread while handling pay_8
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 15000000; i++) n++;
// request pay_8 cannot finish other handlers until this loop returns
```

- homework
```ts
// 7a  pay_8 handled in process A is not in process B's heap
// 7b  two threads in one process can both see a shared array
// 7c  the for-loop is not an await. it does not yield
```

- example 8. process and thread while handling room_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 12000; i++) n++;
// request room_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 8a  room_2 handled in process A is not in process B's heap
// 8b  two threads in one process can both see a shared array
// 8c  the for-loop is not an await. it does not yield
```

- example 9. process and thread while handling vs_7
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 48000; i++) n++;
// request vs_7 cannot finish other handlers until this loop returns
```

- homework
```ts
// 9a  vs_7 handled in process A is not in process B's heap
// 9b  two threads in one process can both see a shared array
// 9c  the for-loop is not an await. it does not yield
```

- example 10. process and thread while handling sc_3
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 11000; i++) n++;
// request sc_3 cannot finish other handlers until this loop returns
```

- homework
```ts
// 10a  sc_3 handled in process A is not in process B's heap
// 10b  two threads in one process can both see a shared array
// 10c  the for-loop is not an await. it does not yield
```

- example 11. process and thread while handling tm_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 2000; i++) n++;
// request tm_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 11a  tm_2 handled in process A is not in process B's heap
// 11b  two threads in one process can both see a shared array
// 11c  the for-loop is not an await. it does not yield
```

- example 12. process and thread while handling up_6
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 200000; i++) n++;
// request up_6 cannot finish other handlers until this loop returns
```

- homework
```ts
// 12a  up_6 handled in process A is not in process B's heap
// 12b  two threads in one process can both see a shared array
// 12c  the for-loop is not an await. it does not yield
```

- example 13. process and thread while handling st_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 1500000; i++) n++;
// request st_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 13a  st_1 handled in process A is not in process B's heap
// 13b  two threads in one process can both see a shared array
// 13c  the for-loop is not an await. it does not yield
```

- example 14. process and thread while handling n_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 24000; i++) n++;
// request n_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 14a  n_2 handled in process A is not in process B's heap
// 14b  two threads in one process can both see a shared array
// 14c  the for-loop is not an await. it does not yield
```

- example 15. process and thread while handling b_3
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 4000; i++) n++;
// request b_3 cannot finish other handlers until this loop returns
```

- homework
```ts
// 15a  b_3 handled in process A is not in process B's heap
// 15b  two threads in one process can both see a shared array
// 15c  the for-loop is not an await. it does not yield
```

- example 16. process and thread while handling se_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 15000; i++) n++;
// request se_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 16a  se_1 handled in process A is not in process B's heap
// 16b  two threads in one process can both see a shared array
// 16c  the for-loop is not an await. it does not yield
```

- example 17. process and thread while handling q_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 10000; i++) n++;
// request q_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 17a  q_1 handled in process A is not in process B's heap
// 17b  two threads in one process can both see a shared array
// 17c  the for-loop is not an await. it does not yield
```

- example 18. process and thread while handling r_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 2000; i++) n++;
// request r_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 18a  r_1 handled in process A is not in process B's heap
// 18b  two threads in one process can both see a shared array
// 18c  the for-loop is not an await. it does not yield
```

- example 19. process and thread while handling pc_12
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 72000; i++) n++;
// request pc_12 cannot finish other handlers until this loop returns
```

- homework
```ts
// 19a  pc_12 handled in process A is not in process B's heap
// 19b  two threads in one process can both see a shared array
// 19c  the for-loop is not an await. it does not yield
```

- example 20. process and thread while handling m_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 3000; i++) n++;
// request m_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 20a  m_1 handled in process A is not in process B's heap
// 20b  two threads in one process can both see a shared array
// 20c  the for-loop is not an await. it does not yield
```

- example 21. process and thread while handling t_9
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 16000; i++) n++;
// request t_9 cannot finish other handlers until this loop returns
```

- homework
```ts
// 21a  t_9 handled in process A is not in process B's heap
// 21b  two threads in one process can both see a shared array
// 21c  the for-loop is not an await. it does not yield
```

- example 22. process and thread while handling v_4
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 6000; i++) n++;
// request v_4 cannot finish other handlers until this loop returns
```

- homework
```ts
// 22a  v_4 handled in process A is not in process B's heap
// 22b  two threads in one process can both see a shared array
// 22c  the for-loop is not an await. it does not yield
```

- example 23. process and thread while handling f_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 1000; i++) n++;
// request f_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 23a  f_2 handled in process A is not in process B's heap
// 23b  two threads in one process can both see a shared array
// 23c  the for-loop is not an await. it does not yield
```

- example 24. process and thread while handling u_3
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 1000; i++) n++;
// request u_3 cannot finish other handlers until this loop returns
```

- homework
```ts
// 24a  u_3 handled in process A is not in process B's heap
// 24b  two threads in one process can both see a shared array
// 24c  the for-loop is not an await. it does not yield
```

- example 25. process and thread while handling pay_8
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 15000000; i++) n++;
// request pay_8 cannot finish other handlers until this loop returns
```

- homework
```ts
// 25a  pay_8 handled in process A is not in process B's heap
// 25b  two threads in one process can both see a shared array
// 25c  the for-loop is not an await. it does not yield
```

- example 26. process and thread while handling room_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 12000; i++) n++;
// request room_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 26a  room_2 handled in process A is not in process B's heap
// 26b  two threads in one process can both see a shared array
// 26c  the for-loop is not an await. it does not yield
```

- example 27. process and thread while handling vs_7
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 48000; i++) n++;
// request vs_7 cannot finish other handlers until this loop returns
```

- homework
```ts
// 27a  vs_7 handled in process A is not in process B's heap
// 27b  two threads in one process can both see a shared array
// 27c  the for-loop is not an await. it does not yield
```

- example 28. process and thread while handling sc_3
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 11000; i++) n++;
// request sc_3 cannot finish other handlers until this loop returns
```

- homework
```ts
// 28a  sc_3 handled in process A is not in process B's heap
// 28b  two threads in one process can both see a shared array
// 28c  the for-loop is not an await. it does not yield
```

- example 29. process and thread while handling tm_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 2000; i++) n++;
// request tm_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 29a  tm_2 handled in process A is not in process B's heap
// 29b  two threads in one process can both see a shared array
// 29c  the for-loop is not an await. it does not yield
```

- example 30. process and thread while handling up_6
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 200000; i++) n++;
// request up_6 cannot finish other handlers until this loop returns
```

- homework
```ts
// 30a  up_6 handled in process A is not in process B's heap
// 30b  two threads in one process can both see a shared array
// 30c  the for-loop is not an await. it does not yield
```

- example 31. process and thread while handling st_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 1500000; i++) n++;
// request st_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 31a  st_1 handled in process A is not in process B's heap
// 31b  two threads in one process can both see a shared array
// 31c  the for-loop is not an await. it does not yield
```

- example 32. process and thread while handling n_2
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 24000; i++) n++;
// request n_2 cannot finish other handlers until this loop returns
```

- homework
```ts
// 32a  n_2 handled in process A is not in process B's heap
// 32b  two threads in one process can both see a shared array
// 32c  the for-loop is not an await. it does not yield
```

- example 33. process and thread while handling b_3
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 4000; i++) n++;
// request b_3 cannot finish other handlers until this loop returns
```

- homework
```ts
// 33a  b_3 handled in process A is not in process B's heap
// 33b  two threads in one process can both see a shared array
// 33c  the for-loop is not an await. it does not yield
```

- example 34. process and thread while handling se_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 15000; i++) n++;
// request se_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 34a  se_1 handled in process A is not in process B's heap
// 34b  two threads in one process can both see a shared array
// 34c  the for-loop is not an await. it does not yield
```

- example 35. process and thread while handling q_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 10000; i++) n++;
// request q_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 35a  q_1 handled in process A is not in process B's heap
// 35b  two threads in one process can both see a shared array
// 35c  the for-loop is not an await. it does not yield
```

- example 36. process and thread while handling r_1
- a process has its own memory. a thread shares that memory
- the loop below blocks every other request on this Node process
- a second PM2 process does not share this JavaScript heap
- during an await, this process can start other work. during the loop, it cannot

```ts
let n = 0;
for (let i = 0; i < 2000; i++) n++;
// request r_1 cannot finish other handlers until this loop returns
```

- homework
```ts
// 36a  r_1 handled in process A is not in process B's heap
// 36b  two threads in one process can both see a shared array
// 36c  the for-loop is not an await. it does not yield
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

- example 1. jobs of 72 ms and 84 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 72 ms, job B = 84 ms
FIFO if A is first: A ends at 72, B ends at 156
a tight loop for pc_12 does not yield its slice early
```

- homework
```text
// 1a  when B finishes under FIFO above
// 1b  what is saved on the switch away from pc_12
// 1c  priority without aging can leave a low job waiting
```

- example 2. jobs of 3 ms and 1 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 3 ms, job B = 1 ms
FIFO if A is first: A ends at 3, B ends at 4
a tight loop for m_1 does not yield its slice early
```

- homework
```text
// 2a  when B finishes under FIFO above
// 2b  what is saved on the switch away from m_1
// 2c  priority without aging can leave a low job waiting
```

- example 3. jobs of 16 ms and 8 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 16 ms, job B = 8 ms
FIFO if A is first: A ends at 16, B ends at 24
a tight loop for t_9 does not yield its slice early
```

- homework
```text
// 3a  when B finishes under FIFO above
// 3b  what is saved on the switch away from t_9
// 3c  priority without aging can leave a low job waiting
```

- example 4. jobs of 6 ms and 10 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 6 ms, job B = 10 ms
FIFO if A is first: A ends at 6, B ends at 16
a tight loop for v_4 does not yield its slice early
```

- homework
```text
// 4a  when B finishes under FIFO above
// 4b  what is saved on the switch away from v_4
// 4c  priority without aging can leave a low job waiting
```

- example 5. jobs of 1 ms and 2 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 1 ms, job B = 2 ms
FIFO if A is first: A ends at 1, B ends at 3
a tight loop for f_2 does not yield its slice early
```

- homework
```text
// 5a  when B finishes under FIFO above
// 5b  what is saved on the switch away from f_2
// 5c  priority without aging can leave a low job waiting
```

- example 6. jobs of 1 ms and 1 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 1 ms, job B = 1 ms
FIFO if A is first: A ends at 1, B ends at 2
a tight loop for u_3 does not yield its slice early
```

- homework
```text
// 6a  when B finishes under FIFO above
// 6b  what is saved on the switch away from u_3
// 6c  priority without aging can leave a low job waiting
```

- example 7. jobs of 15000 ms and 7500 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 15000 ms, job B = 7500 ms
FIFO if A is first: A ends at 15000, B ends at 22500
a tight loop for pay_8 does not yield its slice early
```

- homework
```text
// 7a  when B finishes under FIFO above
// 7b  what is saved on the switch away from pay_8
// 7c  priority without aging can leave a low job waiting
```

- example 8. jobs of 12 ms and 40 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 12 ms, job B = 40 ms
FIFO if A is first: A ends at 12, B ends at 52
a tight loop for room_2 does not yield its slice early
```

- homework
```text
// 8a  when B finishes under FIFO above
// 8b  what is saved on the switch away from room_2
// 8c  priority without aging can leave a low job waiting
```

- example 9. jobs of 48 ms and 60 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 48 ms, job B = 60 ms
FIFO if A is first: A ends at 48, B ends at 108
a tight loop for vs_7 does not yield its slice early
```

- homework
```text
// 9a  when B finishes under FIFO above
// 9b  what is saved on the switch away from vs_7
// 9c  priority without aging can leave a low job waiting
```

- example 10. jobs of 11 ms and 7 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 11 ms, job B = 7 ms
FIFO if A is first: A ends at 11, B ends at 18
a tight loop for sc_3 does not yield its slice early
```

- homework
```text
// 10a  when B finishes under FIFO above
// 10b  what is saved on the switch away from sc_3
// 10c  priority without aging can leave a low job waiting
```

- example 11. jobs of 2 ms and 1 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 2 ms, job B = 1 ms
FIFO if A is first: A ends at 2, B ends at 3
a tight loop for tm_2 does not yield its slice early
```

- homework
```text
// 11a  when B finishes under FIFO above
// 11b  what is saved on the switch away from tm_2
// 11c  priority without aging can leave a low job waiting
```

- example 12. jobs of 200 ms and 6 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 200 ms, job B = 6 ms
FIFO if A is first: A ends at 200, B ends at 206
a tight loop for up_6 does not yield its slice early
```

- homework
```text
// 12a  when B finishes under FIFO above
// 12b  what is saved on the switch away from up_6
// 12c  priority without aging can leave a low job waiting
```

- example 13. jobs of 1500 ms and 1700 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 1500 ms, job B = 1700 ms
FIFO if A is first: A ends at 1500, B ends at 3200
a tight loop for st_1 does not yield its slice early
```

- homework
```text
// 13a  when B finishes under FIFO above
// 13b  what is saved on the switch away from st_1
// 13c  priority without aging can leave a low job waiting
```

- example 14. jobs of 24 ms and 30 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 24 ms, job B = 30 ms
FIFO if A is first: A ends at 24, B ends at 54
a tight loop for n_2 does not yield its slice early
```

- homework
```text
// 14a  when B finishes under FIFO above
// 14b  what is saved on the switch away from n_2
// 14c  priority without aging can leave a low job waiting
```

- example 15. jobs of 4 ms and 2 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 4 ms, job B = 2 ms
FIFO if A is first: A ends at 4, B ends at 6
a tight loop for b_3 does not yield its slice early
```

- homework
```text
// 15a  when B finishes under FIFO above
// 15b  what is saved on the switch away from b_3
// 15c  priority without aging can leave a low job waiting
```

- example 16. jobs of 15 ms and 60 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 15 ms, job B = 60 ms
FIFO if A is first: A ends at 15, B ends at 75
a tight loop for se_1 does not yield its slice early
```

- homework
```text
// 16a  when B finishes under FIFO above
// 16b  what is saved on the switch away from se_1
// 16c  priority without aging can leave a low job waiting
```

- example 17. jobs of 10 ms and 3 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 10 ms, job B = 3 ms
FIFO if A is first: A ends at 10, B ends at 13
a tight loop for q_1 does not yield its slice early
```

- homework
```text
// 17a  when B finishes under FIFO above
// 17b  what is saved on the switch away from q_1
// 17c  priority without aging can leave a low job waiting
```

- example 18. jobs of 2 ms and 4 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 2 ms, job B = 4 ms
FIFO if A is first: A ends at 2, B ends at 6
a tight loop for r_1 does not yield its slice early
```

- homework
```text
// 18a  when B finishes under FIFO above
// 18b  what is saved on the switch away from r_1
// 18c  priority without aging can leave a low job waiting
```

- example 19. jobs of 72 ms and 84 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 72 ms, job B = 84 ms
FIFO if A is first: A ends at 72, B ends at 156
a tight loop for pc_12 does not yield its slice early
```

- homework
```text
// 19a  when B finishes under FIFO above
// 19b  what is saved on the switch away from pc_12
// 19c  priority without aging can leave a low job waiting
```

- example 20. jobs of 3 ms and 1 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 3 ms, job B = 1 ms
FIFO if A is first: A ends at 3, B ends at 4
a tight loop for m_1 does not yield its slice early
```

- homework
```text
// 20a  when B finishes under FIFO above
// 20b  what is saved on the switch away from m_1
// 20c  priority without aging can leave a low job waiting
```

- example 21. jobs of 16 ms and 8 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 16 ms, job B = 8 ms
FIFO if A is first: A ends at 16, B ends at 24
a tight loop for t_9 does not yield its slice early
```

- homework
```text
// 21a  when B finishes under FIFO above
// 21b  what is saved on the switch away from t_9
// 21c  priority without aging can leave a low job waiting
```

- example 22. jobs of 6 ms and 10 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 6 ms, job B = 10 ms
FIFO if A is first: A ends at 6, B ends at 16
a tight loop for v_4 does not yield its slice early
```

- homework
```text
// 22a  when B finishes under FIFO above
// 22b  what is saved on the switch away from v_4
// 22c  priority without aging can leave a low job waiting
```

- example 23. jobs of 1 ms and 2 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 1 ms, job B = 2 ms
FIFO if A is first: A ends at 1, B ends at 3
a tight loop for f_2 does not yield its slice early
```

- homework
```text
// 23a  when B finishes under FIFO above
// 23b  what is saved on the switch away from f_2
// 23c  priority without aging can leave a low job waiting
```

- example 24. jobs of 1 ms and 1 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 1 ms, job B = 1 ms
FIFO if A is first: A ends at 1, B ends at 2
a tight loop for u_3 does not yield its slice early
```

- homework
```text
// 24a  when B finishes under FIFO above
// 24b  what is saved on the switch away from u_3
// 24c  priority without aging can leave a low job waiting
```

- example 25. jobs of 15000 ms and 7500 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 15000 ms, job B = 7500 ms
FIFO if A is first: A ends at 15000, B ends at 22500
a tight loop for pay_8 does not yield its slice early
```

- homework
```text
// 25a  when B finishes under FIFO above
// 25b  what is saved on the switch away from pay_8
// 25c  priority without aging can leave a low job waiting
```

- example 26. jobs of 12 ms and 40 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 12 ms, job B = 40 ms
FIFO if A is first: A ends at 12, B ends at 52
a tight loop for room_2 does not yield its slice early
```

- homework
```text
// 26a  when B finishes under FIFO above
// 26b  what is saved on the switch away from room_2
// 26c  priority without aging can leave a low job waiting
```

- example 27. jobs of 48 ms and 60 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 48 ms, job B = 60 ms
FIFO if A is first: A ends at 48, B ends at 108
a tight loop for vs_7 does not yield its slice early
```

- homework
```text
// 27a  when B finishes under FIFO above
// 27b  what is saved on the switch away from vs_7
// 27c  priority without aging can leave a low job waiting
```

- example 28. jobs of 11 ms and 7 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 11 ms, job B = 7 ms
FIFO if A is first: A ends at 11, B ends at 18
a tight loop for sc_3 does not yield its slice early
```

- homework
```text
// 28a  when B finishes under FIFO above
// 28b  what is saved on the switch away from sc_3
// 28c  priority without aging can leave a low job waiting
```

- example 29. jobs of 2 ms and 1 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 2 ms, job B = 1 ms
FIFO if A is first: A ends at 2, B ends at 3
a tight loop for tm_2 does not yield its slice early
```

- homework
```text
// 29a  when B finishes under FIFO above
// 29b  what is saved on the switch away from tm_2
// 29c  priority without aging can leave a low job waiting
```

- example 30. jobs of 200 ms and 6 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 200 ms, job B = 6 ms
FIFO if A is first: A ends at 200, B ends at 206
a tight loop for up_6 does not yield its slice early
```

- homework
```text
// 30a  when B finishes under FIFO above
// 30b  what is saved on the switch away from up_6
// 30c  priority without aging can leave a low job waiting
```

- example 31. jobs of 1500 ms and 1700 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 1500 ms, job B = 1700 ms
FIFO if A is first: A ends at 1500, B ends at 3200
a tight loop for st_1 does not yield its slice early
```

- homework
```text
// 31a  when B finishes under FIFO above
// 31b  what is saved on the switch away from st_1
// 31c  priority without aging can leave a low job waiting
```

- example 32. jobs of 24 ms and 30 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 24 ms, job B = 30 ms
FIFO if A is first: A ends at 24, B ends at 54
a tight loop for n_2 does not yield its slice early
```

- homework
```text
// 32a  when B finishes under FIFO above
// 32b  what is saved on the switch away from n_2
// 32c  priority without aging can leave a low job waiting
```

- example 33. jobs of 4 ms and 2 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 4 ms, job B = 2 ms
FIFO if A is first: A ends at 4, B ends at 6
a tight loop for b_3 does not yield its slice early
```

- homework
```text
// 33a  when B finishes under FIFO above
// 33b  what is saved on the switch away from b_3
// 33c  priority without aging can leave a low job waiting
```

- example 34. jobs of 15 ms and 60 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 15 ms, job B = 60 ms
FIFO if A is first: A ends at 15, B ends at 75
a tight loop for se_1 does not yield its slice early
```

- homework
```text
// 34a  when B finishes under FIFO above
// 34b  what is saved on the switch away from se_1
// 34c  priority without aging can leave a low job waiting
```

- example 35. jobs of 10 ms and 3 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 10 ms, job B = 3 ms
FIFO if A is first: A ends at 10, B ends at 13
a tight loop for q_1 does not yield its slice early
```

- homework
```text
// 35a  when B finishes under FIFO above
// 35b  what is saved on the switch away from q_1
// 35c  priority without aging can leave a low job waiting
```

- example 36. jobs of 2 ms and 4 ms
- FIFO runs the longer job first if it arrived first
- round robin with a 1 ms slice lets the short job finish earlier
- a context switch saves registers and the stack pointer
- our API is one of the OS jobs, beside nginx and Postgres

```text
job A = 2 ms, job B = 4 ms
FIFO if A is first: A ends at 2, B ends at 6
a tight loop for r_1 does not yield its slice early
```

- homework
```text
// 36a  when B finishes under FIFO above
// 36b  what is saved on the switch away from r_1
// 36c  priority without aging can leave a low job waiting
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

- example 1. two requests both read 72 for pc_12
- the await is the gap. both can write 72+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'pc_12';
```

- homework
```sql
-- 1a  lost value if both write 73 after reading 72
-- 1b  the UPDATE above
-- 1c  lock order for pc_12 and another row: sort the ids first
-- 1d  concurrency on one Node thread still overlaps at await
```

- example 2. two requests both read 3 for m_1
- the await is the gap. both can write 3+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'm_1';
```

- homework
```sql
-- 2a  lost value if both write 4 after reading 3
-- 2b  the UPDATE above
-- 2c  lock order for m_1 and another row: sort the ids first
-- 2d  concurrency on one Node thread still overlaps at await
```

- example 3. two requests both read 16 for t_9
- the await is the gap. both can write 16+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 't_9';
```

- homework
```sql
-- 3a  lost value if both write 17 after reading 16
-- 3b  the UPDATE above
-- 3c  lock order for t_9 and another row: sort the ids first
-- 3d  concurrency on one Node thread still overlaps at await
```

- example 4. two requests both read 6 for v_4
- the await is the gap. both can write 6+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'v_4';
```

- homework
```sql
-- 4a  lost value if both write 7 after reading 6
-- 4b  the UPDATE above
-- 4c  lock order for v_4 and another row: sort the ids first
-- 4d  concurrency on one Node thread still overlaps at await
```

- example 5. two requests both read 1 for f_2
- the await is the gap. both can write 1+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'f_2';
```

- homework
```sql
-- 5a  lost value if both write 2 after reading 1
-- 5b  the UPDATE above
-- 5c  lock order for f_2 and another row: sort the ids first
-- 5d  concurrency on one Node thread still overlaps at await
```

- example 6. two requests both read 1 for u_3
- the await is the gap. both can write 1+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'u_3';
```

- homework
```sql
-- 6a  lost value if both write 2 after reading 1
-- 6b  the UPDATE above
-- 6c  lock order for u_3 and another row: sort the ids first
-- 6d  concurrency on one Node thread still overlaps at await
```

- example 7. two requests both read 15000 for pay_8
- the await is the gap. both can write 15000+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'pay_8';
```

- homework
```sql
-- 7a  lost value if both write 15001 after reading 15000
-- 7b  the UPDATE above
-- 7c  lock order for pay_8 and another row: sort the ids first
-- 7d  concurrency on one Node thread still overlaps at await
```

- example 8. two requests both read 12 for room_2
- the await is the gap. both can write 12+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'room_2';
```

- homework
```sql
-- 8a  lost value if both write 13 after reading 12
-- 8b  the UPDATE above
-- 8c  lock order for room_2 and another row: sort the ids first
-- 8d  concurrency on one Node thread still overlaps at await
```

- example 9. two requests both read 48 for vs_7
- the await is the gap. both can write 48+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'vs_7';
```

- homework
```sql
-- 9a  lost value if both write 49 after reading 48
-- 9b  the UPDATE above
-- 9c  lock order for vs_7 and another row: sort the ids first
-- 9d  concurrency on one Node thread still overlaps at await
```

- example 10. two requests both read 11 for sc_3
- the await is the gap. both can write 11+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'sc_3';
```

- homework
```sql
-- 10a  lost value if both write 12 after reading 11
-- 10b  the UPDATE above
-- 10c  lock order for sc_3 and another row: sort the ids first
-- 10d  concurrency on one Node thread still overlaps at await
```

- example 11. two requests both read 2 for tm_2
- the await is the gap. both can write 2+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'tm_2';
```

- homework
```sql
-- 11a  lost value if both write 3 after reading 2
-- 11b  the UPDATE above
-- 11c  lock order for tm_2 and another row: sort the ids first
-- 11d  concurrency on one Node thread still overlaps at await
```

- example 12. two requests both read 200 for up_6
- the await is the gap. both can write 200+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'up_6';
```

- homework
```sql
-- 12a  lost value if both write 201 after reading 200
-- 12b  the UPDATE above
-- 12c  lock order for up_6 and another row: sort the ids first
-- 12d  concurrency on one Node thread still overlaps at await
```

- example 13. two requests both read 1500 for st_1
- the await is the gap. both can write 1500+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'st_1';
```

- homework
```sql
-- 13a  lost value if both write 1501 after reading 1500
-- 13b  the UPDATE above
-- 13c  lock order for st_1 and another row: sort the ids first
-- 13d  concurrency on one Node thread still overlaps at await
```

- example 14. two requests both read 24 for n_2
- the await is the gap. both can write 24+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'n_2';
```

- homework
```sql
-- 14a  lost value if both write 25 after reading 24
-- 14b  the UPDATE above
-- 14c  lock order for n_2 and another row: sort the ids first
-- 14d  concurrency on one Node thread still overlaps at await
```

- example 15. two requests both read 4 for b_3
- the await is the gap. both can write 4+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'b_3';
```

- homework
```sql
-- 15a  lost value if both write 5 after reading 4
-- 15b  the UPDATE above
-- 15c  lock order for b_3 and another row: sort the ids first
-- 15d  concurrency on one Node thread still overlaps at await
```

- example 16. two requests both read 15 for se_1
- the await is the gap. both can write 15+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'se_1';
```

- homework
```sql
-- 16a  lost value if both write 16 after reading 15
-- 16b  the UPDATE above
-- 16c  lock order for se_1 and another row: sort the ids first
-- 16d  concurrency on one Node thread still overlaps at await
```

- example 17. two requests both read 10 for q_1
- the await is the gap. both can write 10+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'q_1';
```

- homework
```sql
-- 17a  lost value if both write 11 after reading 10
-- 17b  the UPDATE above
-- 17c  lock order for q_1 and another row: sort the ids first
-- 17d  concurrency on one Node thread still overlaps at await
```

- example 18. two requests both read 2 for r_1
- the await is the gap. both can write 2+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'r_1';
```

- homework
```sql
-- 18a  lost value if both write 3 after reading 2
-- 18b  the UPDATE above
-- 18c  lock order for r_1 and another row: sort the ids first
-- 18d  concurrency on one Node thread still overlaps at await
```

- example 19. two requests both read 72 for pc_12
- the await is the gap. both can write 72+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'pc_12';
```

- homework
```sql
-- 19a  lost value if both write 73 after reading 72
-- 19b  the UPDATE above
-- 19c  lock order for pc_12 and another row: sort the ids first
-- 19d  concurrency on one Node thread still overlaps at await
```

- example 20. two requests both read 3 for m_1
- the await is the gap. both can write 3+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'm_1';
```

- homework
```sql
-- 20a  lost value if both write 4 after reading 3
-- 20b  the UPDATE above
-- 20c  lock order for m_1 and another row: sort the ids first
-- 20d  concurrency on one Node thread still overlaps at await
```

- example 21. two requests both read 16 for t_9
- the await is the gap. both can write 16+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 't_9';
```

- homework
```sql
-- 21a  lost value if both write 17 after reading 16
-- 21b  the UPDATE above
-- 21c  lock order for t_9 and another row: sort the ids first
-- 21d  concurrency on one Node thread still overlaps at await
```

- example 22. two requests both read 6 for v_4
- the await is the gap. both can write 6+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'v_4';
```

- homework
```sql
-- 22a  lost value if both write 7 after reading 6
-- 22b  the UPDATE above
-- 22c  lock order for v_4 and another row: sort the ids first
-- 22d  concurrency on one Node thread still overlaps at await
```

- example 23. two requests both read 1 for f_2
- the await is the gap. both can write 1+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'f_2';
```

- homework
```sql
-- 23a  lost value if both write 2 after reading 1
-- 23b  the UPDATE above
-- 23c  lock order for f_2 and another row: sort the ids first
-- 23d  concurrency on one Node thread still overlaps at await
```

- example 24. two requests both read 1 for u_3
- the await is the gap. both can write 1+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'u_3';
```

- homework
```sql
-- 24a  lost value if both write 2 after reading 1
-- 24b  the UPDATE above
-- 24c  lock order for u_3 and another row: sort the ids first
-- 24d  concurrency on one Node thread still overlaps at await
```

- example 25. two requests both read 15000 for pay_8
- the await is the gap. both can write 15000+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'pay_8';
```

- homework
```sql
-- 25a  lost value if both write 15001 after reading 15000
-- 25b  the UPDATE above
-- 25c  lock order for pay_8 and another row: sort the ids first
-- 25d  concurrency on one Node thread still overlaps at await
```

- example 26. two requests both read 12 for room_2
- the await is the gap. both can write 12+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'room_2';
```

- homework
```sql
-- 26a  lost value if both write 13 after reading 12
-- 26b  the UPDATE above
-- 26c  lock order for room_2 and another row: sort the ids first
-- 26d  concurrency on one Node thread still overlaps at await
```

- example 27. two requests both read 48 for vs_7
- the await is the gap. both can write 48+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'vs_7';
```

- homework
```sql
-- 27a  lost value if both write 49 after reading 48
-- 27b  the UPDATE above
-- 27c  lock order for vs_7 and another row: sort the ids first
-- 27d  concurrency on one Node thread still overlaps at await
```

- example 28. two requests both read 11 for sc_3
- the await is the gap. both can write 11+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'sc_3';
```

- homework
```sql
-- 28a  lost value if both write 12 after reading 11
-- 28b  the UPDATE above
-- 28c  lock order for sc_3 and another row: sort the ids first
-- 28d  concurrency on one Node thread still overlaps at await
```

- example 29. two requests both read 2 for tm_2
- the await is the gap. both can write 2+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'tm_2';
```

- homework
```sql
-- 29a  lost value if both write 3 after reading 2
-- 29b  the UPDATE above
-- 29c  lock order for tm_2 and another row: sort the ids first
-- 29d  concurrency on one Node thread still overlaps at await
```

- example 30. two requests both read 200 for up_6
- the await is the gap. both can write 200+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'up_6';
```

- homework
```sql
-- 30a  lost value if both write 201 after reading 200
-- 30b  the UPDATE above
-- 30c  lock order for up_6 and another row: sort the ids first
-- 30d  concurrency on one Node thread still overlaps at await
```

- example 31. two requests both read 1500 for st_1
- the await is the gap. both can write 1500+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'st_1';
```

- homework
```sql
-- 31a  lost value if both write 1501 after reading 1500
-- 31b  the UPDATE above
-- 31c  lock order for st_1 and another row: sort the ids first
-- 31d  concurrency on one Node thread still overlaps at await
```

- example 32. two requests both read 24 for n_2
- the await is the gap. both can write 24+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'n_2';
```

- homework
```sql
-- 32a  lost value if both write 25 after reading 24
-- 32b  the UPDATE above
-- 32c  lock order for n_2 and another row: sort the ids first
-- 32d  concurrency on one Node thread still overlaps at await
```

- example 33. two requests both read 4 for b_3
- the await is the gap. both can write 4+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'b_3';
```

- homework
```sql
-- 33a  lost value if both write 5 after reading 4
-- 33b  the UPDATE above
-- 33c  lock order for b_3 and another row: sort the ids first
-- 33d  concurrency on one Node thread still overlaps at await
```

- example 34. two requests both read 15 for se_1
- the await is the gap. both can write 15+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'se_1';
```

- homework
```sql
-- 34a  lost value if both write 16 after reading 15
-- 34b  the UPDATE above
-- 34c  lock order for se_1 and another row: sort the ids first
-- 34d  concurrency on one Node thread still overlaps at await
```

- example 35. two requests both read 10 for q_1
- the await is the gap. both can write 10+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'q_1';
```

- homework
```sql
-- 35a  lost value if both write 11 after reading 10
-- 35b  the UPDATE above
-- 35c  lock order for q_1 and another row: sort the ids first
-- 35d  concurrency on one Node thread still overlaps at await
```

- example 36. two requests both read 2 for r_1
- the await is the gap. both can write 2+1 and one update is lost
- one SQL statement SET n = n + 1 does not have that gap
- lock rows in id order so two transactions do not form a circle

```sql
UPDATE counters SET n = n + 1 WHERE id = 'r_1';
```

- homework
```sql
-- 36a  lost value if both write 3 after reading 2
-- 36b  the UPDATE above
-- 36c  lock order for r_1 and another row: sort the ids first
-- 36d  concurrency on one Node thread still overlaps at await
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

- example 1. memory for cache key pc_12
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Ocean Star, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("pc_12", "Ocean Star");
// delete the key when pc_12 is no longer needed
```

- homework
```ts
// 1a  heap or stack: the object returned for pc_12
// 1b  a page is often 4 KB
// 1c  RSS grows if pc_12 is never deleted from the Map
```

- example 2. memory for cache key m_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Ada, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("m_1", "Ada");
// delete the key when m_1 is no longer needed
```

- homework
```ts
// 2a  heap or stack: the object returned for m_1
// 2b  a page is often 4 KB
// 2c  RSS grows if m_1 is never deleted from the Map
```

- example 3. memory for cache key t_9
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Rajshahi Open, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("t_9", "Rajshahi Open");
// delete the key when t_9 is no longer needed
```

- homework
```ts
// 3a  heap or stack: the object returned for t_9
// 3b  a page is often 4 KB
// 3c  RSS grows if t_9 is never deleted from the Map
```

- example 4. memory for cache key v_4
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Episode 1, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("v_4", "Episode 1");
// delete the key when v_4 is no longer needed
```

- homework
```ts
// 4a  heap or stack: the object returned for v_4
// 4b  a page is often 4 KB
// 4c  RSS grows if v_4 is never deleted from the Map
```

- example 5. memory for cache key f_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including NOR, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("f_2", "NOR");
// delete the key when f_2 is no longer needed
```

- homework
```ts
// 5a  heap or stack: the object returned for f_2
// 5b  a page is often 4 KB
// 5c  RSS grows if f_2 is never deleted from the Map
```

- example 6. memory for cache key u_3
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including a@example.com, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("u_3", "a@example.com");
// delete the key when u_3 is no longer needed
```

- homework
```ts
// 6a  heap or stack: the object returned for u_3
// 6b  a page is often 4 KB
// 6c  RSS grows if u_3 is never deleted from the Map
```

- example 7. memory for cache key pay_8
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including evt_1, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("pay_8", "evt_1");
// delete the key when pay_8 is no longer needed
```

- homework
```ts
// 7a  heap or stack: the object returned for pay_8
// 7b  a page is often 4 KB
// 7c  RSS grows if pay_8 is never deleted from the Map
```

- example 8. memory for cache key room_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including s_9, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("room_2", "s_9");
// delete the key when room_2 is no longer needed
```

- homework
```ts
// 8a  heap or stack: the object returned for room_2
// 8b  a page is often 4 KB
// 8c  RSS grows if room_2 is never deleted from the Map
```

- example 9. memory for cache key vs_7
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including North Wind, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("vs_7", "North Wind");
// delete the key when vs_7 is no longer needed
```

- homework
```ts
// 9a  heap or stack: the object returned for vs_7
// 9b  a page is often 4 KB
// 9c  RSS grows if vs_7 is never deleted from the Map
```

- example 10. memory for cache key sc_3
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including 11, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("sc_3", "11");
// delete the key when sc_3 is no longer needed
```

- homework
```ts
// 10a  heap or stack: the object returned for sc_3
// 10b  a page is often 4 KB
// 10c  RSS grows if sc_3 is never deleted from the Map
```

- example 11. memory for cache key tm_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Blue, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("tm_2", "Blue");
// delete the key when tm_2 is no longer needed
```

- homework
```ts
// 11a  heap or stack: the object returned for tm_2
// 11b  a page is often 4 KB
// 11c  RSS grows if tm_2 is never deleted from the Map
```

- example 12. memory for cache key up_6
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including videos/u_1/a.mp4, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("up_6", "videos/u_1/a.mp4");
// delete the key when up_6 is no longer needed
```

- homework
```ts
// 12a  heap or stack: the object returned for up_6
// 12b  a page is often 4 KB
// 12c  RSS grows if up_6 is never deleted from the Map
```

- example 13. memory for cache key st_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including player_a, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("st_1", "player_a");
// delete the key when st_1 is no longer needed
```

- homework
```ts
// 13a  heap or stack: the object returned for st_1
// 13b  a page is often 4 KB
// 13c  RSS grows if st_1 is never deleted from the Map
```

- example 14. memory for cache key n_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Chattogram, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("n_2", "Chattogram");
// delete the key when n_2 is no longer needed
```

- homework
```ts
// 14a  heap or stack: the object returned for n_2
// 14b  a page is often 4 KB
// 14c  RSS grows if n_2 is never deleted from the Map
```

- example 15. memory for cache key b_3
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including semi, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("b_3", "semi");
// delete the key when b_3 is no longer needed
```

- homework
```ts
// 15a  heap or stack: the object returned for b_3
// 15b  a page is often 4 KB
// 15c  RSS grows if b_3 is never deleted from the Map
```

- example 16. memory for cache key se_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including u_3, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("se_1", "u_3");
// delete the key when se_1 is no longer needed
```

- homework
```ts
// 16a  heap or stack: the object returned for se_1
// 16b  a page is often 4 KB
// 16c  RSS grows if se_1 is never deleted from the Map
```

- example 17. memory for cache key q_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including laytime, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("q_1", "laytime");
// delete the key when q_1 is no longer needed
```

- homework
```ts
// 17a  heap or stack: the object returned for q_1
// 17b  a page is often 4 KB
// 17c  RSS grows if q_1 is never deleted from the Map
```

- example 18. memory for cache key r_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including operator, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("r_1", "operator");
// delete the key when r_1 is no longer needed
```

- homework
```ts
// 18a  heap or stack: the object returned for r_1
// 18b  a page is often 4 KB
// 18c  RSS grows if r_1 is never deleted from the Map
```

- example 19. memory for cache key pc_12
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Ocean Star, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("pc_12", "Ocean Star");
// delete the key when pc_12 is no longer needed
```

- homework
```ts
// 19a  heap or stack: the object returned for pc_12
// 19b  a page is often 4 KB
// 19c  RSS grows if pc_12 is never deleted from the Map
```

- example 20. memory for cache key m_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Ada, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("m_1", "Ada");
// delete the key when m_1 is no longer needed
```

- homework
```ts
// 20a  heap or stack: the object returned for m_1
// 20b  a page is often 4 KB
// 20c  RSS grows if m_1 is never deleted from the Map
```

- example 21. memory for cache key t_9
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Rajshahi Open, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("t_9", "Rajshahi Open");
// delete the key when t_9 is no longer needed
```

- homework
```ts
// 21a  heap or stack: the object returned for t_9
// 21b  a page is often 4 KB
// 21c  RSS grows if t_9 is never deleted from the Map
```

- example 22. memory for cache key v_4
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Episode 1, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("v_4", "Episode 1");
// delete the key when v_4 is no longer needed
```

- homework
```ts
// 22a  heap or stack: the object returned for v_4
// 22b  a page is often 4 KB
// 22c  RSS grows if v_4 is never deleted from the Map
```

- example 23. memory for cache key f_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including NOR, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("f_2", "NOR");
// delete the key when f_2 is no longer needed
```

- homework
```ts
// 23a  heap or stack: the object returned for f_2
// 23b  a page is often 4 KB
// 23c  RSS grows if f_2 is never deleted from the Map
```

- example 24. memory for cache key u_3
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including a@example.com, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("u_3", "a@example.com");
// delete the key when u_3 is no longer needed
```

- homework
```ts
// 24a  heap or stack: the object returned for u_3
// 24b  a page is often 4 KB
// 24c  RSS grows if u_3 is never deleted from the Map
```

- example 25. memory for cache key pay_8
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including evt_1, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("pay_8", "evt_1");
// delete the key when pay_8 is no longer needed
```

- homework
```ts
// 25a  heap or stack: the object returned for pay_8
// 25b  a page is often 4 KB
// 25c  RSS grows if pay_8 is never deleted from the Map
```

- example 26. memory for cache key room_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including s_9, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("room_2", "s_9");
// delete the key when room_2 is no longer needed
```

- homework
```ts
// 26a  heap or stack: the object returned for room_2
// 26b  a page is often 4 KB
// 26c  RSS grows if room_2 is never deleted from the Map
```

- example 27. memory for cache key vs_7
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including North Wind, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("vs_7", "North Wind");
// delete the key when vs_7 is no longer needed
```

- homework
```ts
// 27a  heap or stack: the object returned for vs_7
// 27b  a page is often 4 KB
// 27c  RSS grows if vs_7 is never deleted from the Map
```

- example 28. memory for cache key sc_3
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including 11, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("sc_3", "11");
// delete the key when sc_3 is no longer needed
```

- homework
```ts
// 28a  heap or stack: the object returned for sc_3
// 28b  a page is often 4 KB
// 28c  RSS grows if sc_3 is never deleted from the Map
```

- example 29. memory for cache key tm_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Blue, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("tm_2", "Blue");
// delete the key when tm_2 is no longer needed
```

- homework
```ts
// 29a  heap or stack: the object returned for tm_2
// 29b  a page is often 4 KB
// 29c  RSS grows if tm_2 is never deleted from the Map
```

- example 30. memory for cache key up_6
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including videos/u_1/a.mp4, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("up_6", "videos/u_1/a.mp4");
// delete the key when up_6 is no longer needed
```

- homework
```ts
// 30a  heap or stack: the object returned for up_6
// 30b  a page is often 4 KB
// 30c  RSS grows if up_6 is never deleted from the Map
```

- example 31. memory for cache key st_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including player_a, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("st_1", "player_a");
// delete the key when st_1 is no longer needed
```

- homework
```ts
// 31a  heap or stack: the object returned for st_1
// 31b  a page is often 4 KB
// 31c  RSS grows if st_1 is never deleted from the Map
```

- example 32. memory for cache key n_2
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including Chattogram, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("n_2", "Chattogram");
// delete the key when n_2 is no longer needed
```

- homework
```ts
// 32a  heap or stack: the object returned for n_2
// 32b  a page is often 4 KB
// 32c  RSS grows if n_2 is never deleted from the Map
```

- example 33. memory for cache key b_3
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including semi, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("b_3", "semi");
// delete the key when b_3 is no longer needed
```

- homework
```ts
// 33a  heap or stack: the object returned for b_3
// 33b  a page is often 4 KB
// 33c  RSS grows if b_3 is never deleted from the Map
```

- example 34. memory for cache key se_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including u_3, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("se_1", "u_3");
// delete the key when se_1 is no longer needed
```

- homework
```ts
// 34a  heap or stack: the object returned for se_1
// 34b  a page is often 4 KB
// 34c  RSS grows if se_1 is never deleted from the Map
```

- example 35. memory for cache key q_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including laytime, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("q_1", "laytime");
// delete the key when q_1 is no longer needed
```

- homework
```ts
// 35a  heap or stack: the object returned for q_1
// 35b  a page is often 4 KB
// 35c  RSS grows if q_1 is never deleted from the Map
```

- example 36. memory for cache key r_1
- virtual pages map to physical frames
- a page fault loads a missing page or crashes on a bad address
- a Map that keeps every body, including operator, grows without a delete
- stack locals die with the function. a returned object lives on the heap

```ts
const cache = new Map<string, string>();
cache.set("r_1", "operator");
// delete the key when r_1 is no longer needed
```

- homework
```ts
// 36a  heap or stack: the object returned for r_1
// 36b  a page is often 4 KB
// 36c  RSS grows if r_1 is never deleted from the Map
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

- example 1. file and system call for Ocean Star
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("Ocean Star") -> fd
read(fd)
close(fd)
name pc_12 is in the directory. the inode is the record
```

- homework
```text
// 1a  inode versus the filename Ocean Star
// 1b  four system calls: open, read, write, close
// 1c  keep pc_12 inside the upload directory
```

- example 2. file and system call for Ada
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("Ada") -> fd
read(fd)
close(fd)
name m_1 is in the directory. the inode is the record
```

- homework
```text
// 2a  inode versus the filename Ada
// 2b  four system calls: open, read, write, close
// 2c  keep m_1 inside the upload directory
```

- example 3. file and system call for Rajshahi Open
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("Rajshahi Open") -> fd
read(fd)
close(fd)
name t_9 is in the directory. the inode is the record
```

- homework
```text
// 3a  inode versus the filename Rajshahi Open
// 3b  four system calls: open, read, write, close
// 3c  keep t_9 inside the upload directory
```

- example 4. file and system call for Episode 1
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("Episode 1") -> fd
read(fd)
close(fd)
name v_4 is in the directory. the inode is the record
```

- homework
```text
// 4a  inode versus the filename Episode 1
// 4b  four system calls: open, read, write, close
// 4c  keep v_4 inside the upload directory
```

- example 5. file and system call for NOR
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("NOR") -> fd
read(fd)
close(fd)
name f_2 is in the directory. the inode is the record
```

- homework
```text
// 5a  inode versus the filename NOR
// 5b  four system calls: open, read, write, close
// 5c  keep f_2 inside the upload directory
```

- example 6. file and system call for a@example.com
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("a@example.com") -> fd
read(fd)
close(fd)
name u_3 is in the directory. the inode is the record
```

- homework
```text
// 6a  inode versus the filename a@example.com
// 6b  four system calls: open, read, write, close
// 6c  keep u_3 inside the upload directory
```

- example 7. file and system call for evt_1
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("evt_1") -> fd
read(fd)
close(fd)
name pay_8 is in the directory. the inode is the record
```

- homework
```text
// 7a  inode versus the filename evt_1
// 7b  four system calls: open, read, write, close
// 7c  keep pay_8 inside the upload directory
```

- example 8. file and system call for s_9
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("s_9") -> fd
read(fd)
close(fd)
name room_2 is in the directory. the inode is the record
```

- homework
```text
// 8a  inode versus the filename s_9
// 8b  four system calls: open, read, write, close
// 8c  keep room_2 inside the upload directory
```

- example 9. file and system call for North Wind
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("North Wind") -> fd
read(fd)
close(fd)
name vs_7 is in the directory. the inode is the record
```

- homework
```text
// 9a  inode versus the filename North Wind
// 9b  four system calls: open, read, write, close
// 9c  keep vs_7 inside the upload directory
```

- example 10. file and system call for 11
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("11") -> fd
read(fd)
close(fd)
name sc_3 is in the directory. the inode is the record
```

- homework
```text
// 10a  inode versus the filename 11
// 10b  four system calls: open, read, write, close
// 10c  keep sc_3 inside the upload directory
```

- example 11. file and system call for Blue
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("Blue") -> fd
read(fd)
close(fd)
name tm_2 is in the directory. the inode is the record
```

- homework
```text
// 11a  inode versus the filename Blue
// 11b  four system calls: open, read, write, close
// 11c  keep tm_2 inside the upload directory
```

- example 12. file and system call for videos/u_1/a.mp4
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("videos/u_1/a.mp4") -> fd
read(fd)
close(fd)
name up_6 is in the directory. the inode is the record
```

- homework
```text
// 12a  inode versus the filename videos/u_1/a.mp4
// 12b  four system calls: open, read, write, close
// 12c  keep up_6 inside the upload directory
```

- example 13. file and system call for player_a
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("player_a") -> fd
read(fd)
close(fd)
name st_1 is in the directory. the inode is the record
```

- homework
```text
// 13a  inode versus the filename player_a
// 13b  four system calls: open, read, write, close
// 13c  keep st_1 inside the upload directory
```

- example 14. file and system call for Chattogram
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("Chattogram") -> fd
read(fd)
close(fd)
name n_2 is in the directory. the inode is the record
```

- homework
```text
// 14a  inode versus the filename Chattogram
// 14b  four system calls: open, read, write, close
// 14c  keep n_2 inside the upload directory
```

- example 15. file and system call for semi
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("semi") -> fd
read(fd)
close(fd)
name b_3 is in the directory. the inode is the record
```

- homework
```text
// 15a  inode versus the filename semi
// 15b  four system calls: open, read, write, close
// 15c  keep b_3 inside the upload directory
```

- example 16. file and system call for u_3
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("u_3") -> fd
read(fd)
close(fd)
name se_1 is in the directory. the inode is the record
```

- homework
```text
// 16a  inode versus the filename u_3
// 16b  four system calls: open, read, write, close
// 16c  keep se_1 inside the upload directory
```

- example 17. file and system call for laytime
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("laytime") -> fd
read(fd)
close(fd)
name q_1 is in the directory. the inode is the record
```

- homework
```text
// 17a  inode versus the filename laytime
// 17b  four system calls: open, read, write, close
// 17c  keep q_1 inside the upload directory
```

- example 18. file and system call for operator
- an inode holds size and blocks. the directory holds the name
- open, read, write, close are system calls Node makes for us
- a user-supplied name must stay inside the upload root. reject a path that climbs out
- deleting a name does not free blocks while a handle is still open

```text
open("operator") -> fd
read(fd)
close(fd)
name r_1 is in the directory. the inode is the record
```

- homework
```text
// 18a  inode versus the filename operator
// 18b  four system calls: open, read, write, close
// 18c  keep r_1 inside the upload directory
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

- example 1. TCP for request pc_12
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for pc_12
- a port distinguishes the program on one IP

```text
client SYN -> server   (pc_12)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /port-calls/pc_12
```

- homework
```text
// 1a  TCP for this HTTP call
// 1b  three packets before the GET of pc_12
// 1c  UDP would not resend a lost laytime update
```

- example 2. TCP for request m_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for m_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (m_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /matches/m_1
```

- homework
```text
// 2a  TCP for this HTTP call
// 2b  three packets before the GET of m_1
// 2c  UDP would not resend a lost laytime update
```

- example 3. TCP for request t_9
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for t_9
- a port distinguishes the program on one IP

```text
client SYN -> server   (t_9)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /tournaments/t_9
```

- homework
```text
// 3a  TCP for this HTTP call
// 3b  three packets before the GET of t_9
// 3c  UDP would not resend a lost laytime update
```

- example 4. TCP for request v_4
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for v_4
- a port distinguishes the program on one IP

```text
client SYN -> server   (v_4)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /videos/v_4
```

- homework
```text
// 4a  TCP for this HTTP call
// 4b  three packets before the GET of v_4
// 4c  UDP would not resend a lost laytime update
```

- example 5. TCP for request f_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for f_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (f_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /facts/f_2
```

- homework
```text
// 5a  TCP for this HTTP call
// 5b  three packets before the GET of f_2
// 5c  UDP would not resend a lost laytime update
```

- example 6. TCP for request u_3
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for u_3
- a port distinguishes the program on one IP

```text
client SYN -> server   (u_3)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /users/u_3
```

- homework
```text
// 6a  TCP for this HTTP call
// 6b  three packets before the GET of u_3
// 6c  UDP would not resend a lost laytime update
```

- example 7. TCP for request pay_8
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for pay_8
- a port distinguishes the program on one IP

```text
client SYN -> server   (pay_8)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /payments/pay_8
```

- homework
```text
// 7a  TCP for this HTTP call
// 7b  three packets before the GET of pay_8
// 7c  UDP would not resend a lost laytime update
```

- example 8. TCP for request room_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for room_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (room_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /rooms/room_2
```

- homework
```text
// 8a  TCP for this HTTP call
// 8b  three packets before the GET of room_2
// 8c  UDP would not resend a lost laytime update
```

- example 9. TCP for request vs_7
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for vs_7
- a port distinguishes the program on one IP

```text
client SYN -> server   (vs_7)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /vessels/vs_7
```

- homework
```text
// 9a  TCP for this HTTP call
// 9b  three packets before the GET of vs_7
// 9c  UDP would not resend a lost laytime update
```

- example 10. TCP for request sc_3
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for sc_3
- a port distinguishes the program on one IP

```text
client SYN -> server   (sc_3)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /scores/sc_3
```

- homework
```text
// 10a  TCP for this HTTP call
// 10b  three packets before the GET of sc_3
// 10c  UDP would not resend a lost laytime update
```

- example 11. TCP for request tm_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for tm_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (tm_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /teams/tm_2
```

- homework
```text
// 11a  TCP for this HTTP call
// 11b  three packets before the GET of tm_2
// 11c  UDP would not resend a lost laytime update
```

- example 12. TCP for request up_6
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for up_6
- a port distinguishes the program on one IP

```text
client SYN -> server   (up_6)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /uploads/up_6
```

- homework
```text
// 12a  TCP for this HTTP call
// 12b  three packets before the GET of up_6
// 12c  UDP would not resend a lost laytime update
```

- example 13. TCP for request st_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for st_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (st_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /standings/st_1
```

- homework
```text
// 13a  TCP for this HTTP call
// 13b  three packets before the GET of st_1
// 13c  UDP would not resend a lost laytime update
```

- example 14. TCP for request n_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for n_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (n_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /notices/n_2
```

- homework
```text
// 14a  TCP for this HTTP call
// 14b  three packets before the GET of n_2
// 14c  UDP would not resend a lost laytime update
```

- example 15. TCP for request b_3
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for b_3
- a port distinguishes the program on one IP

```text
client SYN -> server   (b_3)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /brackets/b_3
```

- homework
```text
// 15a  TCP for this HTTP call
// 15b  three packets before the GET of b_3
// 15c  UDP would not resend a lost laytime update
```

- example 16. TCP for request se_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for se_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (se_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /sessions/se_1
```

- homework
```text
// 16a  TCP for this HTTP call
// 16b  three packets before the GET of se_1
// 16c  UDP would not resend a lost laytime update
```

- example 17. TCP for request q_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for q_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (q_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /queues/q_1
```

- homework
```text
// 17a  TCP for this HTTP call
// 17b  three packets before the GET of q_1
// 17c  UDP would not resend a lost laytime update
```

- example 18. TCP for request r_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for r_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (r_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /roles/r_1
```

- homework
```text
// 18a  TCP for this HTTP call
// 18b  three packets before the GET of r_1
// 18c  UDP would not resend a lost laytime update
```

- example 19. TCP for request pc_12
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for pc_12
- a port distinguishes the program on one IP

```text
client SYN -> server   (pc_12)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /port-calls/pc_12
```

- homework
```text
// 19a  TCP for this HTTP call
// 19b  three packets before the GET of pc_12
// 19c  UDP would not resend a lost laytime update
```

- example 20. TCP for request m_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for m_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (m_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /matches/m_1
```

- homework
```text
// 20a  TCP for this HTTP call
// 20b  three packets before the GET of m_1
// 20c  UDP would not resend a lost laytime update
```

- example 21. TCP for request t_9
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for t_9
- a port distinguishes the program on one IP

```text
client SYN -> server   (t_9)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /tournaments/t_9
```

- homework
```text
// 21a  TCP for this HTTP call
// 21b  three packets before the GET of t_9
// 21c  UDP would not resend a lost laytime update
```

- example 22. TCP for request v_4
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for v_4
- a port distinguishes the program on one IP

```text
client SYN -> server   (v_4)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /videos/v_4
```

- homework
```text
// 22a  TCP for this HTTP call
// 22b  three packets before the GET of v_4
// 22c  UDP would not resend a lost laytime update
```

- example 23. TCP for request f_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for f_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (f_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /facts/f_2
```

- homework
```text
// 23a  TCP for this HTTP call
// 23b  three packets before the GET of f_2
// 23c  UDP would not resend a lost laytime update
```

- example 24. TCP for request u_3
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for u_3
- a port distinguishes the program on one IP

```text
client SYN -> server   (u_3)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /users/u_3
```

- homework
```text
// 24a  TCP for this HTTP call
// 24b  three packets before the GET of u_3
// 24c  UDP would not resend a lost laytime update
```

- example 25. TCP for request pay_8
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for pay_8
- a port distinguishes the program on one IP

```text
client SYN -> server   (pay_8)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /payments/pay_8
```

- homework
```text
// 25a  TCP for this HTTP call
// 25b  three packets before the GET of pay_8
// 25c  UDP would not resend a lost laytime update
```

- example 26. TCP for request room_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for room_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (room_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /rooms/room_2
```

- homework
```text
// 26a  TCP for this HTTP call
// 26b  three packets before the GET of room_2
// 26c  UDP would not resend a lost laytime update
```

- example 27. TCP for request vs_7
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for vs_7
- a port distinguishes the program on one IP

```text
client SYN -> server   (vs_7)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /vessels/vs_7
```

- homework
```text
// 27a  TCP for this HTTP call
// 27b  three packets before the GET of vs_7
// 27c  UDP would not resend a lost laytime update
```

- example 28. TCP for request sc_3
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for sc_3
- a port distinguishes the program on one IP

```text
client SYN -> server   (sc_3)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /scores/sc_3
```

- homework
```text
// 28a  TCP for this HTTP call
// 28b  three packets before the GET of sc_3
// 28c  UDP would not resend a lost laytime update
```

- example 29. TCP for request tm_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for tm_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (tm_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /teams/tm_2
```

- homework
```text
// 29a  TCP for this HTTP call
// 29b  three packets before the GET of tm_2
// 29c  UDP would not resend a lost laytime update
```

- example 30. TCP for request up_6
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for up_6
- a port distinguishes the program on one IP

```text
client SYN -> server   (up_6)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /uploads/up_6
```

- homework
```text
// 30a  TCP for this HTTP call
// 30b  three packets before the GET of up_6
// 30c  UDP would not resend a lost laytime update
```

- example 31. TCP for request st_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for st_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (st_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /standings/st_1
```

- homework
```text
// 31a  TCP for this HTTP call
// 31b  three packets before the GET of st_1
// 31c  UDP would not resend a lost laytime update
```

- example 32. TCP for request n_2
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for n_2
- a port distinguishes the program on one IP

```text
client SYN -> server   (n_2)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /notices/n_2
```

- homework
```text
// 32a  TCP for this HTTP call
// 32b  three packets before the GET of n_2
// 32c  UDP would not resend a lost laytime update
```

- example 33. TCP for request b_3
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for b_3
- a port distinguishes the program on one IP

```text
client SYN -> server   (b_3)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /brackets/b_3
```

- homework
```text
// 33a  TCP for this HTTP call
// 33b  three packets before the GET of b_3
// 33c  UDP would not resend a lost laytime update
```

- example 34. TCP for request se_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for se_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (se_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /sessions/se_1
```

- homework
```text
// 34a  TCP for this HTTP call
// 34b  three packets before the GET of se_1
// 34c  UDP would not resend a lost laytime update
```

- example 35. TCP for request q_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for q_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (q_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /queues/q_1
```

- homework
```text
// 35a  TCP for this HTTP call
// 35b  three packets before the GET of q_1
// 35c  UDP would not resend a lost laytime update
```

- example 36. TCP for request r_1
- OSI is a teaching stack. we use link, IP, TCP or UDP, and the application
- TCP is ordered and resent. UDP is not
- handshake is SYN, SYN-ACK, ACK, then the HTTP bytes for r_1
- a port distinguishes the program on one IP

```text
client SYN -> server   (r_1)
client <- SYN-ACK
client ACK -> server
then the bytes of GET /roles/r_1
```

- homework
```text
// 36a  TCP for this HTTP call
// 36b  three packets before the GET of r_1
// 36c  UDP would not resend a lost laytime update
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

- example 1. name and address for pc_12
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
port-calls.example.  300  IN  A  203.0.113.2
id pc_12 is a name in our API, not an IP
```

- homework
```text
// 1a  /24 size
// 1b  localhost in the API container is not Postgres
// 1c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 2. name and address for m_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
matches.example.  300  IN  A  203.0.113.3
id m_1 is a name in our API, not an IP
```

- homework
```text
// 2a  /24 size
// 2b  localhost in the API container is not Postgres
// 2c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 3. name and address for t_9
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
tournaments.example.  300  IN  A  203.0.113.4
id t_9 is a name in our API, not an IP
```

- homework
```text
// 3a  /24 size
// 3b  localhost in the API container is not Postgres
// 3c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 4. name and address for v_4
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
videos.example.  300  IN  A  203.0.113.5
id v_4 is a name in our API, not an IP
```

- homework
```text
// 4a  /24 size
// 4b  localhost in the API container is not Postgres
// 4c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 5. name and address for f_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
facts.example.  300  IN  A  203.0.113.6
id f_2 is a name in our API, not an IP
```

- homework
```text
// 5a  /24 size
// 5b  localhost in the API container is not Postgres
// 5c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 6. name and address for u_3
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
users.example.  300  IN  A  203.0.113.7
id u_3 is a name in our API, not an IP
```

- homework
```text
// 6a  /24 size
// 6b  localhost in the API container is not Postgres
// 6c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 7. name and address for pay_8
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
payments.example.  300  IN  A  203.0.113.8
id pay_8 is a name in our API, not an IP
```

- homework
```text
// 7a  /24 size
// 7b  localhost in the API container is not Postgres
// 7c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 8. name and address for room_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
rooms.example.  300  IN  A  203.0.113.9
id room_2 is a name in our API, not an IP
```

- homework
```text
// 8a  /24 size
// 8b  localhost in the API container is not Postgres
// 8c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 9. name and address for vs_7
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
vessels.example.  300  IN  A  203.0.113.10
id vs_7 is a name in our API, not an IP
```

- homework
```text
// 9a  /24 size
// 9b  localhost in the API container is not Postgres
// 9c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 10. name and address for sc_3
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
scores.example.  300  IN  A  203.0.113.11
id sc_3 is a name in our API, not an IP
```

- homework
```text
// 10a  /24 size
// 10b  localhost in the API container is not Postgres
// 10c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 11. name and address for tm_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
teams.example.  300  IN  A  203.0.113.12
id tm_2 is a name in our API, not an IP
```

- homework
```text
// 11a  /24 size
// 11b  localhost in the API container is not Postgres
// 11c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 12. name and address for up_6
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
uploads.example.  300  IN  A  203.0.113.13
id up_6 is a name in our API, not an IP
```

- homework
```text
// 12a  /24 size
// 12b  localhost in the API container is not Postgres
// 12c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 13. name and address for st_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
standings.example.  300  IN  A  203.0.113.14
id st_1 is a name in our API, not an IP
```

- homework
```text
// 13a  /24 size
// 13b  localhost in the API container is not Postgres
// 13c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 14. name and address for n_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
notices.example.  300  IN  A  203.0.113.15
id n_2 is a name in our API, not an IP
```

- homework
```text
// 14a  /24 size
// 14b  localhost in the API container is not Postgres
// 14c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 15. name and address for b_3
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
brackets.example.  300  IN  A  203.0.113.16
id b_3 is a name in our API, not an IP
```

- homework
```text
// 15a  /24 size
// 15b  localhost in the API container is not Postgres
// 15c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 16. name and address for se_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
sessions.example.  300  IN  A  203.0.113.17
id se_1 is a name in our API, not an IP
```

- homework
```text
// 16a  /24 size
// 16b  localhost in the API container is not Postgres
// 16c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 17. name and address for q_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
queues.example.  300  IN  A  203.0.113.18
id q_1 is a name in our API, not an IP
```

- homework
```text
// 17a  /24 size
// 17b  localhost in the API container is not Postgres
// 17c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 18. name and address for r_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
roles.example.  300  IN  A  203.0.113.19
id r_1 is a name in our API, not an IP
```

- homework
```text
// 18a  /24 size
// 18b  localhost in the API container is not Postgres
// 18c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 19. name and address for pc_12
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
port-calls.example.  300  IN  A  203.0.113.20
id pc_12 is a name in our API, not an IP
```

- homework
```text
// 19a  /24 size
// 19b  localhost in the API container is not Postgres
// 19c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 20. name and address for m_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
matches.example.  300  IN  A  203.0.113.21
id m_1 is a name in our API, not an IP
```

- homework
```text
// 20a  /24 size
// 20b  localhost in the API container is not Postgres
// 20c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 21. name and address for t_9
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
tournaments.example.  300  IN  A  203.0.113.22
id t_9 is a name in our API, not an IP
```

- homework
```text
// 21a  /24 size
// 21b  localhost in the API container is not Postgres
// 21c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 22. name and address for v_4
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
videos.example.  300  IN  A  203.0.113.23
id v_4 is a name in our API, not an IP
```

- homework
```text
// 22a  /24 size
// 22b  localhost in the API container is not Postgres
// 22c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 23. name and address for f_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
facts.example.  300  IN  A  203.0.113.24
id f_2 is a name in our API, not an IP
```

- homework
```text
// 23a  /24 size
// 23b  localhost in the API container is not Postgres
// 23c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 24. name and address for u_3
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
users.example.  300  IN  A  203.0.113.25
id u_3 is a name in our API, not an IP
```

- homework
```text
// 24a  /24 size
// 24b  localhost in the API container is not Postgres
// 24c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 25. name and address for pay_8
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
payments.example.  300  IN  A  203.0.113.26
id pay_8 is a name in our API, not an IP
```

- homework
```text
// 25a  /24 size
// 25b  localhost in the API container is not Postgres
// 25c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 26. name and address for room_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
rooms.example.  300  IN  A  203.0.113.27
id room_2 is a name in our API, not an IP
```

- homework
```text
// 26a  /24 size
// 26b  localhost in the API container is not Postgres
// 26c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 27. name and address for vs_7
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
vessels.example.  300  IN  A  203.0.113.28
id vs_7 is a name in our API, not an IP
```

- homework
```text
// 27a  /24 size
// 27b  localhost in the API container is not Postgres
// 27c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 28. name and address for sc_3
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
scores.example.  300  IN  A  203.0.113.29
id sc_3 is a name in our API, not an IP
```

- homework
```text
// 28a  /24 size
// 28b  localhost in the API container is not Postgres
// 28c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 29. name and address for tm_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
teams.example.  300  IN  A  203.0.113.30
id tm_2 is a name in our API, not an IP
```

- homework
```text
// 29a  /24 size
// 29b  localhost in the API container is not Postgres
// 29c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 30. name and address for up_6
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
uploads.example.  300  IN  A  203.0.113.31
id up_6 is a name in our API, not an IP
```

- homework
```text
// 30a  /24 size
// 30b  localhost in the API container is not Postgres
// 30c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 31. name and address for st_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
standings.example.  300  IN  A  203.0.113.32
id st_1 is a name in our API, not an IP
```

- homework
```text
// 31a  /24 size
// 31b  localhost in the API container is not Postgres
// 31c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 32. name and address for n_2
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
notices.example.  300  IN  A  203.0.113.33
id n_2 is a name in our API, not an IP
```

- homework
```text
// 32a  /24 size
// 32b  localhost in the API container is not Postgres
// 32c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 33. name and address for b_3
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
brackets.example.  300  IN  A  203.0.113.34
id b_3 is a name in our API, not an IP
```

- homework
```text
// 33a  /24 size
// 33b  localhost in the API container is not Postgres
// 33c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 34. name and address for se_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
sessions.example.  300  IN  A  203.0.113.35
id se_1 is a name in our API, not an IP
```

- homework
```text
// 34a  /24 size
// 34b  localhost in the API container is not Postgres
// 34c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 35. name and address for q_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
queues.example.  300  IN  A  203.0.113.36
id q_1 is a name in our API, not an IP
```

- homework
```text
// 35a  /24 size
// 35b  localhost in the API container is not Postgres
// 35c  TTL 300 seconds keeps the old A record for up to 5 minutes
```

- example 36. name and address for r_1
- a /24 is 256 addresses
- 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are private
- 127.0.0.1 inside a container is that container
- an A record points at an address. a CNAME points at another name
- the TTL is how long a resolver may remember the old address

```text
roles.example.  300  IN  A  203.0.113.37
id r_1 is a name in our API, not an IP
```

- homework
```text
// 36a  /24 size
// 36b  localhost in the API container is not Postgres
// 36c  TTL 300 seconds keeps the old A record for up to 5 minutes
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

- example 1. HTTP and TLS for pc_12
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on pc_12

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 1a  what HTTP/2 multiplexes for pc_12
// 1b  three certificate checks
// 1c  HTTP between nginx and Node on localhost is not the public hop
```

- example 2. HTTP and TLS for m_1
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on m_1

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 2a  what HTTP/2 multiplexes for m_1
// 2b  three certificate checks
// 2c  HTTP between nginx and Node on localhost is not the public hop
```

- example 3. HTTP and TLS for t_9
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on t_9

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 3a  what HTTP/2 multiplexes for t_9
// 3b  three certificate checks
// 3c  HTTP between nginx and Node on localhost is not the public hop
```

- example 4. HTTP and TLS for v_4
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on v_4

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 4a  what HTTP/2 multiplexes for v_4
// 4b  three certificate checks
// 4c  HTTP between nginx and Node on localhost is not the public hop
```

- example 5. HTTP and TLS for f_2
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on f_2

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 5a  what HTTP/2 multiplexes for f_2
// 5b  three certificate checks
// 5c  HTTP between nginx and Node on localhost is not the public hop
```

- example 6. HTTP and TLS for u_3
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on u_3

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 6a  what HTTP/2 multiplexes for u_3
// 6b  three certificate checks
// 6c  HTTP between nginx and Node on localhost is not the public hop
```

- example 7. HTTP and TLS for pay_8
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on pay_8

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 7a  what HTTP/2 multiplexes for pay_8
// 7b  three certificate checks
// 7c  HTTP between nginx and Node on localhost is not the public hop
```

- example 8. HTTP and TLS for room_2
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on room_2

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 8a  what HTTP/2 multiplexes for room_2
// 8b  three certificate checks
// 8c  HTTP between nginx and Node on localhost is not the public hop
```

- example 9. HTTP and TLS for vs_7
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on vs_7

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 9a  what HTTP/2 multiplexes for vs_7
// 9b  three certificate checks
// 9c  HTTP between nginx and Node on localhost is not the public hop
```

- example 10. HTTP and TLS for sc_3
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on sc_3

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 10a  what HTTP/2 multiplexes for sc_3
// 10b  three certificate checks
// 10c  HTTP between nginx and Node on localhost is not the public hop
```

- example 11. HTTP and TLS for tm_2
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on tm_2

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 11a  what HTTP/2 multiplexes for tm_2
// 11b  three certificate checks
// 11c  HTTP between nginx and Node on localhost is not the public hop
```

- example 12. HTTP and TLS for up_6
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on up_6

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 12a  what HTTP/2 multiplexes for up_6
// 12b  three certificate checks
// 12c  HTTP between nginx and Node on localhost is not the public hop
```

- example 13. HTTP and TLS for st_1
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on st_1

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 13a  what HTTP/2 multiplexes for st_1
// 13b  three certificate checks
// 13c  HTTP between nginx and Node on localhost is not the public hop
```

- example 14. HTTP and TLS for n_2
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on n_2

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 14a  what HTTP/2 multiplexes for n_2
// 14b  three certificate checks
// 14c  HTTP between nginx and Node on localhost is not the public hop
```

- example 15. HTTP and TLS for b_3
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on b_3

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 15a  what HTTP/2 multiplexes for b_3
// 15b  three certificate checks
// 15c  HTTP between nginx and Node on localhost is not the public hop
```

- example 16. HTTP and TLS for se_1
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on se_1

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 16a  what HTTP/2 multiplexes for se_1
// 16b  three certificate checks
// 16c  HTTP between nginx and Node on localhost is not the public hop
```

- example 17. HTTP and TLS for q_1
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on q_1

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 17a  what HTTP/2 multiplexes for q_1
// 17b  three certificate checks
// 17c  HTTP between nginx and Node on localhost is not the public hop
```

- example 18. HTTP and TLS for r_1
- HTTP/1.1 does one response at a time on a connection
- HTTP/2 carries many streams on one connection
- the certificate must match the name, be in date, and chain to a trusted root
- nginx can speak HTTP/2 to the browser and HTTP/1.1 to Node
- TLS is the public hop. it does not replace the role check on r_1

```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

- homework
```text
// 18a  what HTTP/2 multiplexes for r_1
// 18b  three certificate checks
// 18c  HTTP between nginx and Node on localhost is not the public hop
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

- example 1. sockets for pc_12
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for pc_12 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3001);
```

- homework
```ts
// 1a  the listen socket is not the client socket for pc_12
// 1b  this snippet is TCP, not HTTP
// 1c  Socket.IO still uses a socket underneath the room watch:pc_12
```

- example 2. sockets for m_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for m_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3002);
```

- homework
```ts
// 2a  the listen socket is not the client socket for m_1
// 2b  this snippet is TCP, not HTTP
// 2c  Socket.IO still uses a socket underneath the room watch:m_1
```

- example 3. sockets for t_9
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for t_9 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3003);
```

- homework
```ts
// 3a  the listen socket is not the client socket for t_9
// 3b  this snippet is TCP, not HTTP
// 3c  Socket.IO still uses a socket underneath the room watch:t_9
```

- example 4. sockets for v_4
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for v_4 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3004);
```

- homework
```ts
// 4a  the listen socket is not the client socket for v_4
// 4b  this snippet is TCP, not HTTP
// 4c  Socket.IO still uses a socket underneath the room watch:v_4
```

- example 5. sockets for f_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for f_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3005);
```

- homework
```ts
// 5a  the listen socket is not the client socket for f_2
// 5b  this snippet is TCP, not HTTP
// 5c  Socket.IO still uses a socket underneath the room watch:f_2
```

- example 6. sockets for u_3
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for u_3 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3006);
```

- homework
```ts
// 6a  the listen socket is not the client socket for u_3
// 6b  this snippet is TCP, not HTTP
// 6c  Socket.IO still uses a socket underneath the room watch:u_3
```

- example 7. sockets for pay_8
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for pay_8 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3007);
```

- homework
```ts
// 7a  the listen socket is not the client socket for pay_8
// 7b  this snippet is TCP, not HTTP
// 7c  Socket.IO still uses a socket underneath the room watch:pay_8
```

- example 8. sockets for room_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for room_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3008);
```

- homework
```ts
// 8a  the listen socket is not the client socket for room_2
// 8b  this snippet is TCP, not HTTP
// 8c  Socket.IO still uses a socket underneath the room watch:room_2
```

- example 9. sockets for vs_7
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for vs_7 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3009);
```

- homework
```ts
// 9a  the listen socket is not the client socket for vs_7
// 9b  this snippet is TCP, not HTTP
// 9c  Socket.IO still uses a socket underneath the room watch:vs_7
```

- example 10. sockets for sc_3
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for sc_3 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3010);
```

- homework
```ts
// 10a  the listen socket is not the client socket for sc_3
// 10b  this snippet is TCP, not HTTP
// 10c  Socket.IO still uses a socket underneath the room watch:sc_3
```

- example 11. sockets for tm_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for tm_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3011);
```

- homework
```ts
// 11a  the listen socket is not the client socket for tm_2
// 11b  this snippet is TCP, not HTTP
// 11c  Socket.IO still uses a socket underneath the room watch:tm_2
```

- example 12. sockets for up_6
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for up_6 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3012);
```

- homework
```ts
// 12a  the listen socket is not the client socket for up_6
// 12b  this snippet is TCP, not HTTP
// 12c  Socket.IO still uses a socket underneath the room watch:up_6
```

- example 13. sockets for st_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for st_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3013);
```

- homework
```ts
// 13a  the listen socket is not the client socket for st_1
// 13b  this snippet is TCP, not HTTP
// 13c  Socket.IO still uses a socket underneath the room watch:st_1
```

- example 14. sockets for n_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for n_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3014);
```

- homework
```ts
// 14a  the listen socket is not the client socket for n_2
// 14b  this snippet is TCP, not HTTP
// 14c  Socket.IO still uses a socket underneath the room watch:n_2
```

- example 15. sockets for b_3
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for b_3 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3015);
```

- homework
```ts
// 15a  the listen socket is not the client socket for b_3
// 15b  this snippet is TCP, not HTTP
// 15c  Socket.IO still uses a socket underneath the room watch:b_3
```

- example 16. sockets for se_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for se_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3016);
```

- homework
```ts
// 16a  the listen socket is not the client socket for se_1
// 16b  this snippet is TCP, not HTTP
// 16c  Socket.IO still uses a socket underneath the room watch:se_1
```

- example 17. sockets for q_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for q_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3017);
```

- homework
```ts
// 17a  the listen socket is not the client socket for q_1
// 17b  this snippet is TCP, not HTTP
// 17c  Socket.IO still uses a socket underneath the room watch:q_1
```

- example 18. sockets for r_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for r_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3018);
```

- homework
```ts
// 18a  the listen socket is not the client socket for r_1
// 18b  this snippet is TCP, not HTTP
// 18c  Socket.IO still uses a socket underneath the room watch:r_1
```

- example 19. sockets for pc_12
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for pc_12 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3019);
```

- homework
```ts
// 19a  the listen socket is not the client socket for pc_12
// 19b  this snippet is TCP, not HTTP
// 19c  Socket.IO still uses a socket underneath the room watch:pc_12
```

- example 20. sockets for m_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for m_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3000);
```

- homework
```ts
// 20a  the listen socket is not the client socket for m_1
// 20b  this snippet is TCP, not HTTP
// 20c  Socket.IO still uses a socket underneath the room watch:m_1
```

- example 21. sockets for t_9
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for t_9 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3001);
```

- homework
```ts
// 21a  the listen socket is not the client socket for t_9
// 21b  this snippet is TCP, not HTTP
// 21c  Socket.IO still uses a socket underneath the room watch:t_9
```

- example 22. sockets for v_4
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for v_4 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3002);
```

- homework
```ts
// 22a  the listen socket is not the client socket for v_4
// 22b  this snippet is TCP, not HTTP
// 22c  Socket.IO still uses a socket underneath the room watch:v_4
```

- example 23. sockets for f_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for f_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3003);
```

- homework
```ts
// 23a  the listen socket is not the client socket for f_2
// 23b  this snippet is TCP, not HTTP
// 23c  Socket.IO still uses a socket underneath the room watch:f_2
```

- example 24. sockets for u_3
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for u_3 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3004);
```

- homework
```ts
// 24a  the listen socket is not the client socket for u_3
// 24b  this snippet is TCP, not HTTP
// 24c  Socket.IO still uses a socket underneath the room watch:u_3
```

- example 25. sockets for pay_8
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for pay_8 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3005);
```

- homework
```ts
// 25a  the listen socket is not the client socket for pay_8
// 25b  this snippet is TCP, not HTTP
// 25c  Socket.IO still uses a socket underneath the room watch:pay_8
```

- example 26. sockets for room_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for room_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3006);
```

- homework
```ts
// 26a  the listen socket is not the client socket for room_2
// 26b  this snippet is TCP, not HTTP
// 26c  Socket.IO still uses a socket underneath the room watch:room_2
```

- example 27. sockets for vs_7
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for vs_7 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3007);
```

- homework
```ts
// 27a  the listen socket is not the client socket for vs_7
// 27b  this snippet is TCP, not HTTP
// 27c  Socket.IO still uses a socket underneath the room watch:vs_7
```

- example 28. sockets for sc_3
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for sc_3 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3008);
```

- homework
```ts
// 28a  the listen socket is not the client socket for sc_3
// 28b  this snippet is TCP, not HTTP
// 28c  Socket.IO still uses a socket underneath the room watch:sc_3
```

- example 29. sockets for tm_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for tm_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3009);
```

- homework
```ts
// 29a  the listen socket is not the client socket for tm_2
// 29b  this snippet is TCP, not HTTP
// 29c  Socket.IO still uses a socket underneath the room watch:tm_2
```

- example 30. sockets for up_6
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for up_6 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3010);
```

- homework
```ts
// 30a  the listen socket is not the client socket for up_6
// 30b  this snippet is TCP, not HTTP
// 30c  Socket.IO still uses a socket underneath the room watch:up_6
```

- example 31. sockets for st_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for st_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3011);
```

- homework
```ts
// 31a  the listen socket is not the client socket for st_1
// 31b  this snippet is TCP, not HTTP
// 31c  Socket.IO still uses a socket underneath the room watch:st_1
```

- example 32. sockets for n_2
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for n_2 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3012);
```

- homework
```ts
// 32a  the listen socket is not the client socket for n_2
// 32b  this snippet is TCP, not HTTP
// 32c  Socket.IO still uses a socket underneath the room watch:n_2
```

- example 33. sockets for b_3
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for b_3 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3013);
```

- homework
```ts
// 33a  the listen socket is not the client socket for b_3
// 33b  this snippet is TCP, not HTTP
// 33c  Socket.IO still uses a socket underneath the room watch:b_3
```

- example 34. sockets for se_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for se_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3014);
```

- homework
```ts
// 34a  the listen socket is not the client socket for se_1
// 34b  this snippet is TCP, not HTTP
// 34c  Socket.IO still uses a socket underneath the room watch:se_1
```

- example 35. sockets for q_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for q_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3015);
```

- homework
```ts
// 35a  the listen socket is not the client socket for q_1
// 35b  this snippet is TCP, not HTTP
// 35c  Socket.IO still uses a socket underneath the room watch:q_1
```

- example 36. sockets for r_1
- listen socket accepts the next client
- accept returns a new socket for that one client
- HTTP and Socket.IO sit on those bytes
- backpressure: pause when the buffer for r_1 is full

```ts
const server = net.createServer((socket) => {
  socket.on("data", (buf) => socket.write(buf));
});
server.listen(3016);
```

- homework
```ts
// 36a  the listen socket is not the client socket for r_1
// 36b  this snippet is TCP, not HTTP
// 36c  Socket.IO still uses a socket underneath the room watch:r_1
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

- example 1. types, garbage, and bytes of "Ocean Star"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Ocean Star";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("pc_12", text);
```

- homework
```ts
// 1a  the compiler deletes the type of vesselName
// 1b  pc_12 stays in memory while the Map holds it
// 1c  text.length and byte length can differ for "Ocean Star"
```

- example 2. types, garbage, and bytes of "Ada"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Ada";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("m_1", text);
```

- homework
```ts
// 2a  the compiler deletes the type of home
// 2b  m_1 stays in memory while the Map holds it
// 2c  text.length and byte length can differ for "Ada"
```

- example 3. types, garbage, and bytes of "Rajshahi Open"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Rajshahi Open";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("t_9", text);
```

- homework
```ts
// 3a  the compiler deletes the type of name
// 3b  t_9 stays in memory while the Map holds it
// 3c  text.length and byte length can differ for "Rajshahi Open"
```

- example 4. types, garbage, and bytes of "Episode 1"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Episode 1";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("v_4", text);
```

- homework
```ts
// 4a  the compiler deletes the type of title
// 4b  v_4 stays in memory while the Map holds it
// 4c  text.length and byte length can differ for "Episode 1"
```

- example 5. types, garbage, and bytes of "NOR"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "NOR";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("f_2", text);
```

- homework
```ts
// 5a  the compiler deletes the type of kind
// 5b  f_2 stays in memory while the Map holds it
// 5c  text.length and byte length can differ for "NOR"
```

- example 6. types, garbage, and bytes of "a@example.com"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "a@example.com";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("u_3", text);
```

- homework
```ts
// 6a  the compiler deletes the type of email
// 6b  u_3 stays in memory while the Map holds it
// 6c  text.length and byte length can differ for "a@example.com"
```

- example 7. types, garbage, and bytes of "evt_1"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "evt_1";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("pay_8", text);
```

- homework
```ts
// 7a  the compiler deletes the type of eventId
// 7b  pay_8 stays in memory while the Map holds it
// 7c  text.length and byte length can differ for "evt_1"
```

- example 8. types, garbage, and bytes of "s_9"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "s_9";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("room_2", text);
```

- homework
```ts
// 8a  the compiler deletes the type of sessionId
// 8b  room_2 stays in memory while the Map holds it
// 8c  text.length and byte length can differ for "s_9"
```

- example 9. types, garbage, and bytes of "North Wind"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "North Wind";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("vs_7", text);
```

- homework
```ts
// 9a  the compiler deletes the type of name
// 9b  vs_7 stays in memory while the Map holds it
// 9c  text.length and byte length can differ for "North Wind"
```

- example 10. types, garbage, and bytes of "11"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "11";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("sc_3", text);
```

- homework
```ts
// 10a  the compiler deletes the type of points
// 10b  sc_3 stays in memory while the Map holds it
// 10c  text.length and byte length can differ for "11"
```

- example 11. types, garbage, and bytes of "Blue"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Blue";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("tm_2", text);
```

- homework
```ts
// 11a  the compiler deletes the type of name
// 11b  tm_2 stays in memory while the Map holds it
// 11c  text.length and byte length can differ for "Blue"
```

- example 12. types, garbage, and bytes of "videos/u_1/a.mp4"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "videos/u_1/a.mp4";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("up_6", text);
```

- homework
```ts
// 12a  the compiler deletes the type of key
// 12b  up_6 stays in memory while the Map holds it
// 12c  text.length and byte length can differ for "videos/u_1/a.mp4"
```

- example 13. types, garbage, and bytes of "player_a"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "player_a";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("st_1", text);
```

- homework
```ts
// 13a  the compiler deletes the type of player
// 13b  st_1 stays in memory while the Map holds it
// 13c  text.length and byte length can differ for "player_a"
```

- example 14. types, garbage, and bytes of "Chattogram"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Chattogram";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("n_2", text);
```

- homework
```ts
// 14a  the compiler deletes the type of port
// 14b  n_2 stays in memory while the Map holds it
// 14c  text.length and byte length can differ for "Chattogram"
```

- example 15. types, garbage, and bytes of "semi"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "semi";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("b_3", text);
```

- homework
```ts
// 15a  the compiler deletes the type of round
// 15b  b_3 stays in memory while the Map holds it
// 15c  text.length and byte length can differ for "semi"
```

- example 16. types, garbage, and bytes of "u_3"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "u_3";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("se_1", text);
```

- homework
```ts
// 16a  the compiler deletes the type of userId
// 16b  se_1 stays in memory while the Map holds it
// 16c  text.length and byte length can differ for "u_3"
```

- example 17. types, garbage, and bytes of "laytime"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "laytime";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("q_1", text);
```

- homework
```ts
// 17a  the compiler deletes the type of name
// 17b  q_1 stays in memory while the Map holds it
// 17c  text.length and byte length can differ for "laytime"
```

- example 18. types, garbage, and bytes of "operator"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "operator";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("r_1", text);
```

- homework
```ts
// 18a  the compiler deletes the type of name
// 18b  r_1 stays in memory while the Map holds it
// 18c  text.length and byte length can differ for "operator"
```

- example 19. types, garbage, and bytes of "Ocean Star"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Ocean Star";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("pc_12", text);
```

- homework
```ts
// 19a  the compiler deletes the type of vesselName
// 19b  pc_12 stays in memory while the Map holds it
// 19c  text.length and byte length can differ for "Ocean Star"
```

- example 20. types, garbage, and bytes of "Ada"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Ada";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("m_1", text);
```

- homework
```ts
// 20a  the compiler deletes the type of home
// 20b  m_1 stays in memory while the Map holds it
// 20c  text.length and byte length can differ for "Ada"
```

- example 21. types, garbage, and bytes of "Rajshahi Open"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Rajshahi Open";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("t_9", text);
```

- homework
```ts
// 21a  the compiler deletes the type of name
// 21b  t_9 stays in memory while the Map holds it
// 21c  text.length and byte length can differ for "Rajshahi Open"
```

- example 22. types, garbage, and bytes of "Episode 1"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Episode 1";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("v_4", text);
```

- homework
```ts
// 22a  the compiler deletes the type of title
// 22b  v_4 stays in memory while the Map holds it
// 22c  text.length and byte length can differ for "Episode 1"
```

- example 23. types, garbage, and bytes of "NOR"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "NOR";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("f_2", text);
```

- homework
```ts
// 23a  the compiler deletes the type of kind
// 23b  f_2 stays in memory while the Map holds it
// 23c  text.length and byte length can differ for "NOR"
```

- example 24. types, garbage, and bytes of "a@example.com"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "a@example.com";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("u_3", text);
```

- homework
```ts
// 24a  the compiler deletes the type of email
// 24b  u_3 stays in memory while the Map holds it
// 24c  text.length and byte length can differ for "a@example.com"
```

- example 25. types, garbage, and bytes of "evt_1"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "evt_1";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("pay_8", text);
```

- homework
```ts
// 25a  the compiler deletes the type of eventId
// 25b  pay_8 stays in memory while the Map holds it
// 25c  text.length and byte length can differ for "evt_1"
```

- example 26. types, garbage, and bytes of "s_9"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "s_9";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("room_2", text);
```

- homework
```ts
// 26a  the compiler deletes the type of sessionId
// 26b  room_2 stays in memory while the Map holds it
// 26c  text.length and byte length can differ for "s_9"
```

- example 27. types, garbage, and bytes of "North Wind"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "North Wind";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("vs_7", text);
```

- homework
```ts
// 27a  the compiler deletes the type of name
// 27b  vs_7 stays in memory while the Map holds it
// 27c  text.length and byte length can differ for "North Wind"
```

- example 28. types, garbage, and bytes of "11"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "11";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("sc_3", text);
```

- homework
```ts
// 28a  the compiler deletes the type of points
// 28b  sc_3 stays in memory while the Map holds it
// 28c  text.length and byte length can differ for "11"
```

- example 29. types, garbage, and bytes of "Blue"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Blue";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("tm_2", text);
```

- homework
```ts
// 29a  the compiler deletes the type of name
// 29b  tm_2 stays in memory while the Map holds it
// 29c  text.length and byte length can differ for "Blue"
```

- example 30. types, garbage, and bytes of "videos/u_1/a.mp4"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "videos/u_1/a.mp4";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("up_6", text);
```

- homework
```ts
// 30a  the compiler deletes the type of key
// 30b  up_6 stays in memory while the Map holds it
// 30c  text.length and byte length can differ for "videos/u_1/a.mp4"
```

- example 31. types, garbage, and bytes of "player_a"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "player_a";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("st_1", text);
```

- homework
```ts
// 31a  the compiler deletes the type of player
// 31b  st_1 stays in memory while the Map holds it
// 31c  text.length and byte length can differ for "player_a"
```

- example 32. types, garbage, and bytes of "Chattogram"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "Chattogram";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("n_2", text);
```

- homework
```ts
// 32a  the compiler deletes the type of port
// 32b  n_2 stays in memory while the Map holds it
// 32c  text.length and byte length can differ for "Chattogram"
```

- example 33. types, garbage, and bytes of "semi"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "semi";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("b_3", text);
```

- homework
```ts
// 33a  the compiler deletes the type of round
// 33b  b_3 stays in memory while the Map holds it
// 33c  text.length and byte length can differ for "semi"
```

- example 34. types, garbage, and bytes of "u_3"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "u_3";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("se_1", text);
```

- homework
```ts
// 34a  the compiler deletes the type of userId
// 34b  se_1 stays in memory while the Map holds it
// 34c  text.length and byte length can differ for "u_3"
```

- example 35. types, garbage, and bytes of "laytime"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "laytime";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("q_1", text);
```

- homework
```ts
// 35a  the compiler deletes the type of name
// 35b  q_1 stays in memory while the Map holds it
// 35c  text.length and byte length can differ for "laytime"
```

- example 36. types, garbage, and bytes of "operator"
- TypeScript erases the types. the running code is JavaScript
- a value still reachable from a Map is not garbage
- UTF-8 byte length can be larger than the number of characters
- JSON on the wire is UTF-8

```ts
const text = "operator";
Buffer.byteLength(text, "utf8");
const keep = new Map<string, string>();
keep.set("r_1", text);
```

- homework
```ts
// 36a  the compiler deletes the type of name
// 36b  r_1 stays in memory while the Map holds it
// 36c  text.length and byte length can differ for "operator"
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

- example 1. hops for GET /port-calls/pc_12
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // pc_12
pool
Postgres
```

- homework
```text
// 1a  list the hops for pc_12
// 1b  the await on Prisma is when another request can run
// 1c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 2. hops for GET /matches/m_1
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // m_1
pool
Postgres
```

- homework
```text
// 2a  list the hops for m_1
// 2b  the await on Prisma is when another request can run
// 2c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 3. hops for GET /tournaments/t_9
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // t_9
pool
Postgres
```

- homework
```text
// 3a  list the hops for t_9
// 3b  the await on Prisma is when another request can run
// 3c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 4. hops for GET /videos/v_4
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // v_4
pool
Postgres
```

- homework
```text
// 4a  list the hops for v_4
// 4b  the await on Prisma is when another request can run
// 4c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 5. hops for GET /facts/f_2
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // f_2
pool
Postgres
```

- homework
```text
// 5a  list the hops for f_2
// 5b  the await on Prisma is when another request can run
// 5c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 6. hops for GET /users/u_3
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // u_3
pool
Postgres
```

- homework
```text
// 6a  list the hops for u_3
// 6b  the await on Prisma is when another request can run
// 6c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 7. hops for GET /payments/pay_8
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // pay_8
pool
Postgres
```

- homework
```text
// 7a  list the hops for pay_8
// 7b  the await on Prisma is when another request can run
// 7c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 8. hops for GET /rooms/room_2
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // room_2
pool
Postgres
```

- homework
```text
// 8a  list the hops for room_2
// 8b  the await on Prisma is when another request can run
// 8c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 9. hops for GET /vessels/vs_7
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // vs_7
pool
Postgres
```

- homework
```text
// 9a  list the hops for vs_7
// 9b  the await on Prisma is when another request can run
// 9c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 10. hops for GET /scores/sc_3
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // sc_3
pool
Postgres
```

- homework
```text
// 10a  list the hops for sc_3
// 10b  the await on Prisma is when another request can run
// 10c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 11. hops for GET /teams/tm_2
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // tm_2
pool
Postgres
```

- homework
```text
// 11a  list the hops for tm_2
// 11b  the await on Prisma is when another request can run
// 11c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 12. hops for GET /uploads/up_6
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // up_6
pool
Postgres
```

- homework
```text
// 12a  list the hops for up_6
// 12b  the await on Prisma is when another request can run
// 12c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 13. hops for GET /standings/st_1
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // st_1
pool
Postgres
```

- homework
```text
// 13a  list the hops for st_1
// 13b  the await on Prisma is when another request can run
// 13c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 14. hops for GET /notices/n_2
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // n_2
pool
Postgres
```

- homework
```text
// 14a  list the hops for n_2
// 14b  the await on Prisma is when another request can run
// 14c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 15. hops for GET /brackets/b_3
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // b_3
pool
Postgres
```

- homework
```text
// 15a  list the hops for b_3
// 15b  the await on Prisma is when another request can run
// 15c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 16. hops for GET /sessions/se_1
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // se_1
pool
Postgres
```

- homework
```text
// 16a  list the hops for se_1
// 16b  the await on Prisma is when another request can run
// 16c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 17. hops for GET /queues/q_1
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // q_1
pool
Postgres
```

- homework
```text
// 17a  list the hops for q_1
// 17b  the await on Prisma is when another request can run
// 17c  two Node processes do not share a JavaScript lock. they share Postgres
```

- example 18. hops for GET /roles/r_1
- DNS, TCP, TLS, nginx, Node, pool, Postgres
- the JavaScript thread is free at the await
- the row lock, if we take one, lives in Postgres

```text
browser
DNS
TCP + TLS
nginx
Node  // r_1
pool
Postgres
```

- homework
```text
// 18a  list the hops for r_1
// 18b  the await on Prisma is when another request can run
// 18c  two Node processes do not share a JavaScript lock. they share Postgres
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

- example 1. sizes beside pc_12
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id pc_12
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 1a  packets before HTTP for pc_12
// 1b  isolation if we set nothing
// 1c  127.0.0.1 in the API container is that container, not pc_12's database
```

- example 2. sizes beside m_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id m_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 2a  packets before HTTP for m_1
// 2b  isolation if we set nothing
// 2c  127.0.0.1 in the API container is that container, not m_1's database
```

- example 3. sizes beside t_9
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id t_9
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 3a  packets before HTTP for t_9
// 3b  isolation if we set nothing
// 3c  127.0.0.1 in the API container is that container, not t_9's database
```

- example 4. sizes beside v_4
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id v_4
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 4a  packets before HTTP for v_4
// 4b  isolation if we set nothing
// 4c  127.0.0.1 in the API container is that container, not v_4's database
```

- example 5. sizes beside f_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id f_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 5a  packets before HTTP for f_2
// 5b  isolation if we set nothing
// 5c  127.0.0.1 in the API container is that container, not f_2's database
```

- example 6. sizes beside u_3
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id u_3
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 6a  packets before HTTP for u_3
// 6b  isolation if we set nothing
// 6c  127.0.0.1 in the API container is that container, not u_3's database
```

- example 7. sizes beside pay_8
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id pay_8
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 7a  packets before HTTP for pay_8
// 7b  isolation if we set nothing
// 7c  127.0.0.1 in the API container is that container, not pay_8's database
```

- example 8. sizes beside room_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id room_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 8a  packets before HTTP for room_2
// 8b  isolation if we set nothing
// 8c  127.0.0.1 in the API container is that container, not room_2's database
```

- example 9. sizes beside vs_7
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id vs_7
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 9a  packets before HTTP for vs_7
// 9b  isolation if we set nothing
// 9c  127.0.0.1 in the API container is that container, not vs_7's database
```

- example 10. sizes beside sc_3
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id sc_3
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 10a  packets before HTTP for sc_3
// 10b  isolation if we set nothing
// 10c  127.0.0.1 in the API container is that container, not sc_3's database
```

- example 11. sizes beside tm_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id tm_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 11a  packets before HTTP for tm_2
// 11b  isolation if we set nothing
// 11c  127.0.0.1 in the API container is that container, not tm_2's database
```

- example 12. sizes beside up_6
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id up_6
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 12a  packets before HTTP for up_6
// 12b  isolation if we set nothing
// 12c  127.0.0.1 in the API container is that container, not up_6's database
```

- example 13. sizes beside st_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id st_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 13a  packets before HTTP for st_1
// 13b  isolation if we set nothing
// 13c  127.0.0.1 in the API container is that container, not st_1's database
```

- example 14. sizes beside n_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id n_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 14a  packets before HTTP for n_2
// 14b  isolation if we set nothing
// 14c  127.0.0.1 in the API container is that container, not n_2's database
```

- example 15. sizes beside b_3
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id b_3
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 15a  packets before HTTP for b_3
// 15b  isolation if we set nothing
// 15c  127.0.0.1 in the API container is that container, not b_3's database
```

- example 16. sizes beside se_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id se_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 16a  packets before HTTP for se_1
// 16b  isolation if we set nothing
// 16c  127.0.0.1 in the API container is that container, not se_1's database
```

- example 17. sizes beside q_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id q_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 17a  packets before HTTP for q_1
// 17b  isolation if we set nothing
// 17c  127.0.0.1 in the API container is that container, not q_1's database
```

- example 18. sizes beside r_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id r_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 18a  packets before HTTP for r_1
// 18b  isolation if we set nothing
// 18c  127.0.0.1 in the API container is that container, not r_1's database
```

- example 19. sizes beside pc_12
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id pc_12
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 19a  packets before HTTP for pc_12
// 19b  isolation if we set nothing
// 19c  127.0.0.1 in the API container is that container, not pc_12's database
```

- example 20. sizes beside m_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id m_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 20a  packets before HTTP for m_1
// 20b  isolation if we set nothing
// 20c  127.0.0.1 in the API container is that container, not m_1's database
```

- example 21. sizes beside t_9
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id t_9
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 21a  packets before HTTP for t_9
// 21b  isolation if we set nothing
// 21c  127.0.0.1 in the API container is that container, not t_9's database
```

- example 22. sizes beside v_4
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id v_4
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 22a  packets before HTTP for v_4
// 22b  isolation if we set nothing
// 22c  127.0.0.1 in the API container is that container, not v_4's database
```

- example 23. sizes beside f_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id f_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 23a  packets before HTTP for f_2
// 23b  isolation if we set nothing
// 23c  127.0.0.1 in the API container is that container, not f_2's database
```

- example 24. sizes beside u_3
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id u_3
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 24a  packets before HTTP for u_3
// 24b  isolation if we set nothing
// 24c  127.0.0.1 in the API container is that container, not u_3's database
```

- example 25. sizes beside pay_8
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id pay_8
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 25a  packets before HTTP for pay_8
// 25b  isolation if we set nothing
// 25c  127.0.0.1 in the API container is that container, not pay_8's database
```

- example 26. sizes beside room_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id room_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 26a  packets before HTTP for room_2
// 26b  isolation if we set nothing
// 26c  127.0.0.1 in the API container is that container, not room_2's database
```

- example 27. sizes beside vs_7
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id vs_7
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 27a  packets before HTTP for vs_7
// 27b  isolation if we set nothing
// 27c  127.0.0.1 in the API container is that container, not vs_7's database
```

- example 28. sizes beside sc_3
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id sc_3
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 28a  packets before HTTP for sc_3
// 28b  isolation if we set nothing
// 28c  127.0.0.1 in the API container is that container, not sc_3's database
```

- example 29. sizes beside tm_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id tm_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 29a  packets before HTTP for tm_2
// 29b  isolation if we set nothing
// 29c  127.0.0.1 in the API container is that container, not tm_2's database
```

- example 30. sizes beside up_6
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id up_6
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 30a  packets before HTTP for up_6
// 30b  isolation if we set nothing
// 30c  127.0.0.1 in the API container is that container, not up_6's database
```

- example 31. sizes beside st_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id st_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 31a  packets before HTTP for st_1
// 31b  isolation if we set nothing
// 31c  127.0.0.1 in the API container is that container, not st_1's database
```

- example 32. sizes beside n_2
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id n_2
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 32a  packets before HTTP for n_2
// 32b  isolation if we set nothing
// 32c  127.0.0.1 in the API container is that container, not n_2's database
```

- example 33. sizes beside b_3
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id b_3
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 33a  packets before HTTP for b_3
// 33b  isolation if we set nothing
// 33c  127.0.0.1 in the API container is that container, not b_3's database
```

- example 34. sizes beside se_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id se_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 34a  packets before HTTP for se_1
// 34b  isolation if we set nothing
// 34c  127.0.0.1 in the API container is that container, not se_1's database
```

- example 35. sizes beside q_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id q_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 35a  packets before HTTP for q_1
// 35b  isolation if we set nothing
// 35c  127.0.0.1 in the API container is that container, not q_1's database
```

- example 36. sizes beside r_1
- TCP handshake is 3 packets
- a common page is 4 KB
- a /24 is 256 addresses
- Postgres default isolation is read committed
- UTF-8 is the JSON encoding
- day length for estimates is about 100,000 seconds

```text
id r_1
handshake 3
page 4096
/24 256
isolation read committed
```

- homework
```text
// 36a  packets before HTTP for r_1
// 36b  isolation if we set nothing
// 36c  127.0.0.1 in the API container is that container, not r_1's database
```
