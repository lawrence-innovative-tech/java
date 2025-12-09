
#### **Stream
- Stream is data pipeline process. 
- Without terminal operation it not start to process.
- Stream it used to process or manipulate the datasource without modifying the datasource.

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
