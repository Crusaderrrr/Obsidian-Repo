---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
These are a **sequence of elements to perform some operations**, such as filtering, mapping, etc.
Same as a **conveyer** with items (elements) on it, which are coming from somewhere (collection, list, object, etc.).

Streams are indeed a sequence of elements and, for example, are used to handle input of the file, from internet or other sources and this sequence is very large, streams will read the data *piece by piece*, rather than loading an entire file or whatever. 

## There are two types of Operations in Streams:
1. **Intermediate Operations**
	Intermediate Operations are the types of operations in which multiple methods are chained in a row. They transform a stream into another stream.
2. **Terminal Operations**
	Terminal Operations are the type of Operations that return the result. These Operations are not processed further just return a final result value.

# Intermediate Operations
```java
// map
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
// filter
Stream<T> filter(Predicate<? super T> predicate)
// sorted
Stream<T> sorted()  
Stream<T> sorted(Comparator<? super T> comparator)
// flatMap
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
// distinct
Stream<T> distinct()
// peek
Stream<T> peek(Consumer<? super T> action)
```

- `flatMap(List::stream)`: Flattens a stream of collections into a single stream of elements.
- `filter(s -> s.startsWith("S"))`: selects elements as per the Predicate passed as an argument.
- `map()`: returns a stream consisting of the results of applying the given function to the elements of this stream.
- `distinct()`: Removes any duplicate strings.
- `sorted()`: sorts the stream.
- `peek(...)`: Performs an action on each element without modifying the stream. It returns a stream consisting of the elements of this stream, additionally performing the provided action on each element as elements are consumed from the resulting stream.
- `collect(Collectors.toList())`: Collects the final processed strings into a list called result.

# Terminal Operations
```java
// collect
<R, A> R collect(Collector<? super T, A, R> collector)
// forEach
void forEach(Consumer<? super T> action)
// reduce
T reduce(T identity, BinaryOperator<T> accumulator)  
Optional<T> reduce(BinaryOperator<T> accumulator)
// count
long count()
// findFirst
Optional<T> findFirst()
// allMatch
boolean allMatch(Predicate<? super T> predicate)
// anyMatch
boolean anyMatch(Predicate<? super T> predicate)
```
- `collect()` Returns the result of the intermediate operations performed on the stream.
- `forEach()` Iterates through every element of the stream.
- `reduce()` Reduces the elements of a stream to a single value. The reduce method takes a BinaryOperator as a parameter.
- `count()` Returns the count of elements in the stream.
- `findFirst()` Returns the first element of the stream, if present.
- `allMatch()` Checks if all elements of the stream match a given predicate.
- `anyMatch()` Checks if any element of the stream matches a given predicate.