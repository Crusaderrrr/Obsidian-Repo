Simple parser that makes requests to the api of some service. 

Steps:
- initialization, makes an api call and extracts metadata from it (total number of pages)
- creates a `FixedThreadPool`, which is basically the place where some threads (5) are created with a queue of tasks
- loop over number of pages and `supplyAsync()`, which adds a page to the queue
- thread 1 takes a task from queue and works with it
	- task 2 is passed to queue, if thread 1 is busy, thread 2 takes it
	- etc.
- every thread (future) persists all the collected data in memory
- main thread loops over all the futures and saves the data to the database

This could be problematic, because a lot of data is kept in memory after parsing -> **potential improvement**

70k investors is approximately *~150–200 MB* of memory. 