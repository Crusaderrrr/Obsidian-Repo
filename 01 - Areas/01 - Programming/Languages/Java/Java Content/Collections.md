---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
This is a Java [[Framework]] — a unified architecture in Java that provides a set of **interfaces**, **classes**, and **algorithms** to store, organize, manipulate, and access groups of objects in a standardized way. It simplifies working with different types of collections like lists, sets, queues, and maps by providing a consistent API and reusable data structures.

It has this structure:  
![[Pasted image 20250813125553.png]]

There is an **Iterable Interface**, which isn’t in this diagram, but it is the **root interface** of the whole framework — all other collection interfaces and classes implement it.  
Its main functionality is to provide an _iterator_ for collections.

---

# 6 Main Interfaces
These are used to implement all the data type classes, e.g. HashSet, ArrayList, etc.

- **Collection**
- **List**
- **Queue**
- **Deque** (Double-ended queue)
- **Set**
- **Map**

---

## **Collection Interface**

Contains all the **basic methods** common to all collections, e.g.:
- Adding elements
- Removing elements
- Clearing all elements
- Bulk operations like `addAll()`, `removeAll()`, `containsAll()`, `retainAll()`

---

## **List Interface**

Child interface of Collection. Keeps elements **ordered** and allows **positional (index-based) access**.
## Implementations:

1. **ArrayList**
    - Dynamic array
    - Auto-resizes when adding/removing elements

2. **LinkedList**
    - Doubly linked list; each node (element) has data + pointers to next and previous
        
3. **Vector** (Legacy)
    - Dynamic array, synchronized
    - Slow for single-threaded use; replaced by ArrayList
        
4. **Stack** (Legacy)
    - LIFO structure; inherits from `Vector`
        
5. **AbstractList**
    - Partial reusable implementation of `List`
        
6. **AbstractSequentialList**
    - Extends AbstractList
    - Optimized for sequential access (linked lists)
        

---

## **Set Interface**

*Unordered* collection of unique elements (no duplicates).

![[Pasted image 20250813181314.png]]
## Implementations:

1. **HashSet**
    - Backed by a hash table
    - No guaranteed order of iteration
        
2. **AbstractSet**
    - Skeleton implementation that provides `equals()` and `hashCode()`
        
3. **CopyOnWriteArraySet**
    - Thread-safe set backed by CopyOnWriteArrayList
    - Multi-threaded use
    - Read operations > write operations 
        
4. **LinkedHashSet**
    - Maintains insertion order (uses a linked list + hash table)
        
### **SortedSet Interface**

Specialization of Set — maintains *sorted order* of elements. Extends a Set Interface.
## Implementations:

1. **TreeSet**
    - Red-Black tree
    - Natural ordering or custom comparator
        
2. **NavigableSet** (Interface)
    - Extends SortedSet with navigation methods:
        - `lower()`, `floor()`, `ceiling()`, `higher()`
            
3. **ConcurrentSkipListSet**
	- Implementation of NavigableSet 
    - Thread-safe and sorted (based on Skip List algorithm)
        

---

## **Map Interface**

Stores *key-value pairs* (like Python’s `dict`).  
Keys must be *unique*, values can be duplicate.  
Internally often implemented using hashing.  
On hash collisions, values are stored in a *linked list* or *balanced tree* at that bucket.

![[Pasted image 20250814160800.png]]

## Implementations:

1. **Hashtable** (Legacy)
    - Synchronized, thread-safe
    - No null keys or null values
        
2. **HashMap**
    - Unsynchronized, better performance
    - Allows one null key & multiple null values
        
3. **LinkedHashMap**
    - Maintains insertion order (uses linked list + hash table)
        
4. **ConcurrentHashMap**
    - Thread-safe with better concurrency than Hashtable
        
5. **TreeMap**
    - Sorted map using Red-Black tree
    - Keys sorted naturally or via Comparator
        
6. **EnumMap**
    - Specialized map for enum keys (very fast)
        
7. **AbstractMap**
    - Skeleton implementation of the Map interface
        
### **SortedMap Interface**

Extends Map to keep keys sorted.

- **NavigableMap**: Adds navigation methods like `lowerKey()`, `floorKey()`, etc.
    

---

## **Queue Interface**

Maintains **FIFO order** (unless priority rules apply).  
Used when order of processing matters.

## Implementations:

1. **PriorityQueue**
    - Based on a heap structure
    - Orders elements by priority
        
2. **ArrayDeque**
    - Resizable array, faster than `Stack` for LIFO
        
3. **ConcurrentLinkedQueue**
    - Thread-safe, non-blocking
        
4. **BlockingQueue** Implementations:
    - **ArrayBlockingQueue** (bounded)
    - **LinkedBlockingQueue** (optionally bounded)
    - **PriorityBlockingQueue** (unbounded, priority-ordered)
    - **DelayQueue** (time-based release)
    - **LinkedTransferQueue** (transfer elements between threads)
        

---

## **Deque Interface**

Double-ended queue — elements can be added and removed from *both ends*.
Used when flexible queue operations on both ends needed.

## Implementations:

- **ArrayDeque**
    
- **ConcurrentLinkedDeque**
    
- **BlockingDeque** (thread-safe blocking operations)

--- 

> [!note] Blocking Queue

This is a kind of queue, which is used for multiple threads and it blocks producing or consuming if it is either full or empty.
