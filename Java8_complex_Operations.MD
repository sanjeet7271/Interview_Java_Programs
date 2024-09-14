# Uses of Stream.of()
    In Java 8, you can use Stream.of() to create a stream from a fixed set of values.:
    1. Creating a Stream from Individual Elements:
        Stream<Integer> numbers = Stream.of(1, 2, 3, 4, 5); 
        Stream<String> names = Stream.of("Alice", "Bob", "Charlie");
    2. Creating a Stream from an Array:
        Integer[] numbersArray = {1, 2, 3, 4, 5};
        Stream<Integer> numbers = Stream.of(numbersArray);
    3. 

## Uses of PartitioningBy
        The partitioningBy() method always returns a Map with two entries - one for where the Predicate is true, and one for when it's false. Both entries can have empty lists, but they will be present.
        Example:
        public class PartitionBy {
            public static void main(String[] args) {
                Stream<Integer> listStream= Stream.of(1,2,3,4,5,6,6,7,8,9);
                Map<Boolean, List<Integer>> booleanListMap = listStream.collect(Collectors.partitioningBy(n -> n % 2 == 0));
                System.out.println(booleanListMap);
            }
        }
    Use Counting to count number of numbers are in true and false
        Map<Boolean, Long> booleanListMapCounting = Stream.of(10,15,20,25,30,35,40,45,50,55,60,65).collect(Collectors.partitioningBy(n -> n % 2 == 0, Collectors.counting()));
        System.out.println(booleanListMapCounting);
