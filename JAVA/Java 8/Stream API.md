
#### **Stream
- Stream is data pipeline process. 
- Without terminal operation it not start to process.
- Stream it used to process or manipulate the datasource without modifying the datasource.
- If the stream runs one time it never allow to run again that stream.

##### **Three Major part of stream
1. [[#**Several types to create stream object,|Creation part]]
2. [[#**Intermediate Stream|Intermediate Part]]
3. [[#**Terminal Stream|Terminal Part]]
##### **Sub part of stream //TODO
1. Spliterator  
##### **Several types to create stream object

1. Collection.stream() -- creates collection object used to create stream object.
2. Stream.of()  -- creates passing arguments in of() methods creates stream object.
3. Arrays.stream -- creates primitive object to stream object, and it called boxing.
4. Files.readlines / BufferReader.lines -- creates stream object.
5. Pattern.spiltAsStream().
6. Stream.generate() -- creates infinity condition based stream.
7. Stream.iterate() -- creates infinity count based stream.
8. Primitive stream()
##### **Intermediate Stream

##### **Filtering and Truncating Operations

|Operation|Signature|Description|Introduced|
|---|---|---|---|
|**filter**|`Stream<T> filter(Predicate<? super T> predicate)`|Returns elements matching the predicate.|Java 8|
|**takeWhile**|`Stream<T> takeWhile(Predicate<? super T> predicate)`|Takes the longest prefix of elements matching the predicate (ordered streams only).|Java 9|
|**dropWhile**|`Stream<T> dropWhile(Predicate<? super T> predicate)`|Drops the longest prefix of elements matching the predicate (ordered streams only).|Java 9|
|**limit**|`Stream<T> limit(long maxSize)`|Truncates to the first `maxSize` elements.|Java 8|
|**skip**|`Stream<T> skip(long n)`|Discards the first `n` elements.|Java 8|

##### **Mapping Operations

|Operation|Signature|Description|Introduced|
|---|---|---|---|
|**map**|`<R> Stream<R> map(Function<? super T, ? extends R> mapper)`|Transforms each element using the mapper (1:1).|Java 8|
|**mapToInt**|`IntStream mapToInt(ToIntFunction<? super T> mapper)`|Maps to primitive `int` values (avoids boxing).|Java 8|
|**mapToLong**|`LongStream mapToLong(ToLongFunction<? super T> mapper)`|Maps to primitive `long` values.|Java 8|
|**mapToDouble**|`DoubleStream mapToDouble(ToDoubleFunction<? super T> mapper)`|Maps to primitive `double` values.|Java 8|
|**flatMap**|`<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)`|Flattens nested streams (1:many).|Java 8|
|**flatMapToInt**|`IntStream flatMapToInt(Function<? super T, ? extends IntStream> mapper)`|Flattens to primitive `IntStream`.|Java 8|
|**flatMapToLong**|`LongStream flatMapToLong(Function<? super T, ? extends LongStream> mapper)`|Flattens to primitive `LongStream`.|Java 8|
|**flatMapToDouble**|`DoubleStream flatMapToDouble(Function<? super T, ? extends DoubleStream> mapper)`|Flattens to primitive `DoubleStream`.|Java 8|
|**mapMulti**|`<R> Stream<R> mapMulti(BiConsumer<? super T, ? super Consumer<R>> mapper)`|Maps each element to zero or more elements (advanced flattening).|Java 16|
|**mapMultiToInt**|`IntStream mapMultiToInt(BiConsumer<? super T, ? super IntConsumer> mapper)`|Maps to zero or more primitive `int` values.|Java 16|
|**mapMultiToLong**|`LongStream mapMultiToLong(BiConsumer<? super T, ? super LongConsumer> mapper)`|Maps to zero or more primitive `long` values.|Java 16|
|**mapMultiToDouble**|`DoubleStream mapMultiToDouble(BiConsumer<? super T, ? super DoubleConsumer> mapper)`|Maps to zero or more primitive `double` values.|Java 16|

##### **Deduplicating and Sorting Operations

|Operation|Signature|Description|Introduced|
|---|---|---|---|
|**distinct**|`Stream<T> distinct()`|Removes duplicate elements based on `equals()`.|Java 8|
|**sorted**|`Stream<T> sorted()`|Sorts elements in natural order.|Java 8|
|**sorted**|`Stream<T> sorted(Comparator<? super T> comparator)`|Sorts elements using a custom comparator.|Java 8|

##### **Peeking and Gathering Operations

|Operation|Signature|Description|Introduced|
|---|---|---|---|
|**peek**|`Stream<T> peek(Consumer<? super T> action)`|Performs an action (e.g., logging) on each element without modifying it.|Java 8|
|**gather**|`<R> Stream<R> gather(Gatherer<? super T, ?, R> gatherer)`|Applies a custom gatherer for complex transformations (experimental in earlier previews).|Java 24|

##### **Terminal Stream
- When terminal operation only start the execution of stream pipeline, and if terminal operation has involved streams has end.
- Some Terminal operation list,

| Operation        | Signature                                                                                              | Return Type   | Description                                                                  |
| ---------------- | ------------------------------------------------------------------------------------------------------ | ------------- | ---------------------------------------------------------------------------- |
| `forEach`        | `void forEach(Consumer<? super T> action)`                                                             | `void`        | Performs an action for each element (nondeterministic in parallel streams).  |
| `forEachOrdered` | `void forEachOrdered(Consumer<? super T> action)`                                                      | `void`        | Performs an action for each element, respecting encounter order.             |
| `toArray`        | `Object[] toArray()`                                                                                   | `Object[]`    | Returns a runtime Object array of stream elements.                           |
| `toArray`        | `<A> A[] toArray(IntFunction<A[]> generator)`                                                          | `A[]`         | Returns an array using a provided generator function.                        |
| `reduce`         | `Optional<T> reduce(BinaryOperator<T> accumulator)`                                                    | `Optional<T>` | Reduces elements to a single value using an accumulator (associative).       |
| `reduce`         | `T reduce(T identity, BinaryOperator<T> accumulator)`                                                  | `T`           | Reduces with an identity value and accumulator.                              |
| `reduce`         | `<U> U reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)`        | `U`           | Reduces with identity, accumulator, and combiner (for parallel).             |
| `collect`        | `<R, A> R collect(Collector<? super T, A, R> collector)`                                               | `R`           | Accumulates into a result using a Collector (e.g., `toList()`, `joining()`). |
| `collect`        | `<R> R collect(Supplier<R> supplier, BiConsumer<R, ? super T> accumulator, BiConsumer<R, R> combiner)` | `R`           | Mutable reduction with explicit supplier, accumulator, and combiner.         |
| `toList`         | `default List<T> toList()`                                                                             | `List<T>`     | Collects elements into an unmodifiable `List` (Java 16+).                    |
| `min`            | `Optional<T> min(Comparator<? super T> comparator)`                                                    | `Optional<T>` | Returns the minimum element per comparator (empty if stream empty).          |
| `max`            | `Optional<T> max(Comparator<? super T> comparator)`                                                    | `Optional<T>` | Returns the maximum element per comparator (empty if stream empty).          |
| `count`          | `long count()`                                                                                         | `long`        | Returns the number of elements in the stream.                                |
| `anyMatch`*      | `boolean anyMatch(Predicate<? super T> predicate)`                                                     | `boolean`     | Returns `true` if any element matches the predicate.                         |
| `allMatch`*      | `boolean allMatch(Predicate<? super T> predicate)`                                                     | `boolean`     | Returns `true` if all elements match (or stream empty).                      |
| `noneMatch`*     | `boolean noneMatch(Predicate<? super T> predicate)`                                                    | `boolean`     | Returns `true` if no elements match (or stream empty).                       |
| `findFirst`*     | `Optional<T> findFirst()`                                                                              | `Optional<T>` | Returns the first element (respects order).                                  |
| `findAny`*       | `Optional<T> findAny()`                                                                                | `Optional<T>` | Returns any element (nondeterministic, good for parallel).                   |