
This is a special mechanism in JVM which **deletes objects and strings** from the heap **that do not have a reference**. 

- We can barely control it (only ask to review)
- There is an hierarchy of the variables, which helps with optimization: 
	- *Young generation*:
		- Eden - are gonna be deleted 
		- S0 - survivors 
		- S1 - survivors 
	- *Old generation*:
		- Tenured 
Young generation is small and fast to scan.

### How a young collection runs

1. Objects allocated in Eden.
2. Eden fills → a **minor GC** triggers.
3. Live objects copied to a survivor space; dead ones vanish (the whole Eden is just declared empty — no per-object cleanup).
4. Objects surviving enough rounds get promoted to old gen.

## How does it know what to collect

GC does not walk through objects, it **walks though all the references from the root**, dead objects are never visited.

# GC Algorithms

### Serial GC (**STOP-THE-WORLD**)
- Single thread does everything, and the entire app freezes during collection (stop-the-world). No parallelism, no concurrency.
- **Analogy:** One person cleaning the whole house alone while everyone else waits outside. Fine for a studio apartment, hopeless for a mansion.
- Use: simple CLI apps. Lowest overhead, simplest, but pauses grow with heap size.

### Parallel GC *a.k.a. Throughput Collector* (**stop-the-world**)
- Still stop-the-world, but multiple threads do the collection at once. Optimizes for **total throughput** — get GC done fast, maximize app time between pauses — not for short individual pauses.
- Use: batch jobs, data processing, anything where total run time matters more than any single pause

### G1 (Garbage-First) — **the default since Java 9**

Splits the heap into many equal **regions** instead of fixed contiguous young/old blocks. It tracks which regions hold the most garbage and collects those _first_ (hence the name), aiming to hit a **pause-time target** you set (e.g. "keep pauses under 200ms"). Marking is largely concurrent; the actual evacuation pauses are short and incremental.

Use: the general-purpose default — server apps, mid-to-large heaps where you want balanced, predictable pauses. Spring Boot services almost certainly run this.

### ZGC (**flash**)
A **concurrent, low-latency** collector. Does nearly all its work _while the app keeps running_, using colored pointers and load barriers to relocate objects without stopping the world. Pause times are sub-millisecond and — the headline feature — **stay flat regardless of heap size**, whether 10GB or multiple terabytes.

Use: latency-critical services on large heaps (low-latency APIs, trading-adjacent systems, huge in-memory datasets). *The cost is more CPU and memory* overhead spent on that concurrent bookkeeping, so raw throughput can be lower than Parallel.