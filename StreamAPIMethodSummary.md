
# Stream APIs

## Consumer
: It represents a function which accepts one parameter and does not return anything.
## Supplier
: It represents a function which does not accepts any parameter and returns a result.
## Predicate
: It represents a function which accepts one parameter and returns either true or false based on some condition.

## Stream conversion
### Arrays
- `Arrays.stream(arr)`
- `Stream.of(arr)`
### List
- `Collection.stream()` - example, `list.stream()`
### Map
- There is no direct method to do this. Generally we create a stream of entrySet of the map by map.entrySet().stream()
### Specified values
- `Stream.of(1,2,3,4,5,6)`
### Empty Stream
- `Stream.empty()`
### Infinite stream
- `Stream.iterate(seedValue, (Integer n) -> n*n).limit(limitValue)` - seedValue is the first element in the stream, and the function passed will be applied on to this seedValue for every subsequent element, limit operator applies the limit to the number of elements in the stream.
- `Stream.generate(Supplier fucntion).limit(limitValue)` - The supplier function is used to generate values of this stream and limit is used to limit the number of elements in the stream, example, Stream.generate(Math::random).limit(5) will generate stream of random numbers upto 5 elements.

## Operations
- `filter(Predicate)`
: Filters the stream as per the passed Predicate and returns the new filtered stream.
- `map(Function)`
: Applies the passed function to the elements and returns the new stream.
- `mapToInt(Function)`
: It returns an IntStream consisting of the results of applying the given function to the elements of this stream.
- `mapToLong(Function)`
: It returns a LongStream consisting of the results of applying the given function to the elements of this stream.
- `mapToDouble(Function)`
: It returns a DoubleStream consisting of the results of applying the given function to the elements of this stream.
- `flatMap(Function)`
: It returns a stream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element. Each mapped stream is closed after its contents have been placed into this stream. (If a mapped stream is null an empty stream is used, instead.)
- `flatMapToInt(Function)`
: It returns an IntStream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element. Each mapped stream is closed after its contents have been placed into this stream. (If a mapped stream is null an empty stream is used, instead.)
- `flatMapToLong(Function)`
: It returns a LongStream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element. Each mapped stream is closed after its contents have been placed into this stream. (If a mapped stream is null an empty stream is used, instead.)
- `flatMapToDouble(Function)`
: It returns a DoubleStream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element. Each mapped stream is closed after its contents have placed been into this stream. (If a mapped stream is null an empty stream is used, instead.)
- `forEach(Consumer)`
: It performs an action for each element of this stream.
- `forEachOrdered(Consumer)`
: It performs an action for each element of this stream, in the encounter order of the stream if the stream has a defined encounter order.
- `sum()`
: It returns the sum of elements in this stream. This is a special case of a reduction. IntStream sum() is a terminal operation i.e, it may traverse the stream to produce a result or a side-effect. 
- `reduce(BinaryOperator)`
: It performs a reduction on the elements of this stream, using an associative accumulation function, and returns an Optional describing the reduced value, if any.
- `reduce(T identity, BinaryOperator)`
: It performs a reduction on the elements of this stream, using the provided identity value and an associative accumulation function, and returns the reduced value.
- `reduce(T identity, BiFunctino accumulator, BinaryOperator)`
: It performs a reduction on the elements of this stream, using the provided identity, accumulation and combining functions.
- `skip(long n)`
: It returns a stream consisting of the remaining elements of this stream after discarding the first n elements of the stream. If this stream contains fewer than n elements then an empty stream will be returned.
- `sorted()`
: It returns a stream consisting of the elements of this stream, sorted according to natural order. If the elements of this stream are not Comparable, a java.lang.ClassCastException may be thrown when the terminal operation is executed.
- `sorted(Comparator)
: It returns a stream consisting of the elements of this stream, sorted according to the provided Comparator.
- `collect(Collector)`
: It performs a mutable reduction operation on the elements of this stream using a Collector. A Collector encapsulates the functions used as arguments to collect(Supplier, BiConsumer, BiConsumer), allowing for reuse of collection strategies and composition of collect operations such as multiple-level grouping or partitioning.
	- `collect(Supplier, BiConsumer<R,? super T> accumulator, BiConsumer<R,R> combiner)`
		- It performs a mutable reduction operation on the elements of this stream. A mutable reduction is one in which the reduced value is a mutable result 
		  container, such as an ArrayList, and elements are incorporated by updating the state of the result rather than by replacing the result.
	- `concat(Stream<? of T> a, Stream<? of T> b)`
		- It creates a lazily concatenated stream whose elements are all the elements of the first stream followed by all the elements of the second stream. 
		  The resulting stream is ordered if both of the input streams are ordered, and parallel if either of the input streams is parallel. When the resulting stream is closed, the close handlers for both input streams are invoked.
	- `toArray()`
		- It returns an array containing the elements of this stream.
	- `toArray(IntFunction generator)`
		- It returns an array containing the elements of this stream, using the provided generator function to allocate the returned array, as well as any 
		  additional arrays that might be required for a partitioned execution or for resizing.
	- `max(Comparator)`
		- It returns the maximum element of this stream according to the provided Comparator. This is a special case of a reduction. Returns optional.
	- `min(Comparator)`
		- It returns the minimum element of this stream according to the provided Comparator. This is a special case of a reduction. Returns optional.
	- `distinct()`
		- It returns a stream consisting of the distinct elements (according to Object.equals(Object)) of this stream.
	- `findAny()`
		- It returns an Optional describing some element of the stream, or an empty Optional if the stream is empty.
	- `findFirst()`
		- It returns an Optional describing the first element of this stream, or an empty Optional if the stream is empty. If the stream has no encounter order, then any element may be returned.
	- `allMatch(Predicate)`
		-	Returns all the elements which matches the passed predicate. If the stream is empty, true is returned and the predicate is not evaluated.
	- `anyMatch(Predicate)`
		-	Returns any element which matches the passed predicate. If the stream is empty, trus is returned and the predicate is not evaluated.
	- `noneMatch(Predicate)`
		- It returns elements of this stream match the provided predicate. If the stream is empty then true is returned and the predicate is not evaluated.
	- `count()`
		- It returns the count of elements in this stream. This is a special case of a reduction.
	- `limit(long maxSize)`
		- It returns a stream consisting of the elements of this stream, truncated to be no longer than maxSize in length.

## Collectors
	- `toCollection(Supplier)
		- Transforms the input elements into a new Collection, and returns a Collector.
	- `toList()`
		- Transforms the input elements into a new List and returns a Collector.
	- `toSet()`
		- Transforms the input elements into a new Set and returns a Collector. This method will return Set instance and it doesn’t contain any duplicates.
	- `toMap(Function keyMapper, Function valueMapper, BinaryOpertaor[optional], Supplier[optional])
		- Transforms the elements into a Map whose keys and values are the results of applying the passed mapper functions to the input elements and returns a 
		  Collector. BinaryOpertor handles the duplicate keys, and Supplier enables the user to create a user expected Map implementation, example,
		  `Collectors.toMap(obj -> obj.key, obj -> obj.value, (obj1, obj2) -> obj1.key, HashMap::new)`
	- `counting()`
		- It counts the number of input elements of type T and returns a Collector. This method is used in a case where we want to group and count the number 
		  of times each city is present in the collection of elements.
	- `collectionAndThen(Collector, Function finisher)`
		- This method allows us to perform another operation on the result after collecting the input element of collection.
	- `groupingBy(Function finisher)`
		- Performs group by operation on input elements of type T. The grouping of elements is done as per the passed classifier function and returns the 
		  Collector with result in a Map.
	- `groupingBy(Function finisher, Collector)`
		- Performs group by operation on input elements of type T. The grouping of the elements is done as per the passed classifier function and then performs 
		  a reduction operation on the values associated with a given key as per the specified downstream Collector and returns the Collector with result in a Map.
	- `groupingBy(Function finisher, Supplier, Collector)`
		- Performs group by operation on input elements of type T, the grouping of elements is done as per the passed classifier function and then performs a 
		  reduction operation on the values associated with a given key as per the specified downstream Collector and returns the Collector.
	- `joining()`
		- Concatenates the input elements into a String and returns a Collector.
	- `joining(CharSequence delimiter)`
		- Concatenates the input elements, separated by the specified delimiter, and returns a Collector.
	- `joining(CharSequence delimiter, CharSequence prefix, CharSequence suffix)`
		- Concatenates the input elements, separated by the specified delimiter, as per the specified prefix and suffix, and returns a Collector.
	- `mapping(Functin mapper, Collector downstream)`
		- Transforms a Collector of the input elements of type U to one the input elements of type T by applying a mapping function to every input element 
		  before the transformation.
	- `partitioningBy(Predicate)`
		- Partitions the input elements as per the passed Predicate, and transforms them into a Map and returns the Collector.
	- `partitioningBy(Predicate, Collector)`
		- Partitions the input elements as per the passed Predicate, and collects the values of each partition as per another Collector, and transforms them 
		  into a Map whose values are the results of the downstream reduction and then return Collector.
	- `averagingDouble(ToDoubleFunction mapper)`
		- Performs the average of the input elements of type Double, and returns the Collector as a result.
	- `averagingInt(ToIntFunction mapper)`
		- Performs the average of the input elements of type Int, and returns the Collector as a result.
	- `averagingLing(ToLongFunction mapper)`
		- Performs the average of the input elements of type Long, and returns the Collector as a result.
	- `reducing(BinaryOperator)`
		- Performs a reduction of its input elements as per passed BinaryOperator and returns a Collector.
	- `reducing(T identity, BinaryOpertor)`
		- Performs a reduction of its input elements as per passed BinaryOperator and as per the passed identity and returns Collector.
	- `maxBy(Comparator)`
		- Produces the maximal element as per given Comparator, returns an Optional Collector.
	- `minBy(Comparator)`
		- Produces the minimal element as per given Comparator, returns an Optional Collector.
