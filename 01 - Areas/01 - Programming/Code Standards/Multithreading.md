This is hard to build a solid "clean" multithreaded program. 
- [[Concurrent Programming|Concurrent Code]] is not intuitively understood, it often acts very different to a single threaded code, consequently it is hard to test, *because some tests that pass today will fail tomorrow*. 
- **Concurrency is a design problem, not the optimization**.


### Shared state
- This is one of the most important problems 
- Many bugs come from situations when many threads access the same state and read/write it
- **Solution**: make shared state as small as possible
- Protect if shared state is necessary: `synchronyzed`, locks, etc.

### Problems I will encounter
There are 3 types according to the book:
1. **Producer-Consumer** — one thread produces work, another consumes it. The boundary between them (typically a queue) needs careful synchronization
2. **Readers-Writers** — multiple threads read, occasional threads write. Writers need exclusive access; readers can share. Getting the balance wrong causes either starvation (writers never get in) or stale reads.
3. **Dining Philosophers** — the classic deadlock scenario. Threads compete for multiple resources, and if each holds one while waiting for another, everything grinds to a halt. Relevant whenever your code acquires more than one lock.

### Practical Rules to Actually Follow
- Isolate business logic code and multithreading code
- Do not share more then you need to
- Know your library (it is necessary to investigate how the library works, and it is logically understood)

### Testing 
As said before, it is almost impossible to test, as **bugs are timing-dependent** and **often non-reproducible**.
- Write tests that can expose problems, then run them frequently under varied conditions
- Concurrent bugs that only appear in production are the worst kind. Invest in testing infrastructure early rather than assuming "it worked in my tests."

