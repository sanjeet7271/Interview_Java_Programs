# Java Map Sorting Using Streams --- Interview Notes

## 1. Program: Sort Map by Key and Value

This program demonstrates how to:

-   Remove `null` keys and `null` values from a `Map`
-   Sort a `Map` by key in ascending order
-   Sort a `Map` by key in descending order
-   Sort a `Map` by value in ascending order
-   Sort a `Map` by value in descending order
-   Preserve sorted order using `LinkedHashMap`

### Complete Program

``` java
package Collections;

import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.stream.Collectors;

public class SortByKeyAndValueInMap {
    public static void main(String[] args) {

        Map<String, Integer> map = new HashMap<>();

        map.put("Santosh", 124);
        map.put("Raj", 634);
        map.put("Aman", 645);
        map.put("Manjit", 91);
        map.put("Baba", null);
        map.put(null, 96);

        // Remove null key and null value
        map = map.entrySet().stream()
                .filter(entry -> entry.getKey() != null && entry.getValue() != null)
                .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue
                ));

        System.out.println("After removing null values: " + map);

        // Ascending Order by Key
        Map<String, Integer> sortByKeyByASC = map.entrySet().stream()
                .sorted(Map.Entry.comparingByKey())
                .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue,
                        (a, b) -> a,
                        LinkedHashMap::new
                ));

        System.out.println("Key ASC: " + sortByKeyByASC);

        // Descending Order by Key
        Map<String, Integer> sortByKeyByDESC = map.entrySet().stream()
                .sorted(Map.Entry.<String, Integer>comparingByKey().reversed())
                .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue,
                        (a, b) -> a,
                        LinkedHashMap::new
                ));

        System.out.println("Key DESC: " + sortByKeyByDESC);

        // Ascending Order by Value
        Map<String, Integer> sortByValueASC = map.entrySet().stream()
                .sorted(Map.Entry.comparingByValue())
                .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue,
                        (a, b) -> a,
                        LinkedHashMap::new
                ));

        System.out.println("Value ASC: " + sortByValueASC);

        // Descending Order by Value
        Map<String, Integer> sortedByValueDESC = map.entrySet().stream()
                .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
                .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue,
                        (a, b) -> a,
                        LinkedHashMap::new
                ));

        System.out.println("Value DESC: " + sortedByValueDESC);
    }
}
```

------------------------------------------------------------------------

# 2. Expected Output

After removing the `null` key and `null` value:

``` text
{Santosh=124, Raj=634, Aman=645, Manjit=91}
```

### Key Ascending

``` text
{Aman=645, Manjit=91, Raj=634, Santosh=124}
```

### Key Descending

``` text
{Santosh=124, Raj=634, Manjit=91, Aman=645}
```

### Value Ascending

``` text
{Manjit=91, Santosh=124, Raj=634, Aman=645}
```

### Value Descending

``` text
{Aman=645, Raj=634, Santosh=124, Manjit=91}
```

> Note: The initial `HashMap` does not guarantee insertion order. The
> sorted results use `LinkedHashMap` so the stream's sorted order is
> preserved.

------------------------------------------------------------------------

# 3. Important Concepts

## `entrySet()`

``` java
map.entrySet()
```

Returns all key-value pairs as `Map.Entry` objects.

For example:

``` text
Santosh=124
Raj=634
Aman=645
Manjit=91
```

Each entry contains:

``` java
entry.getKey()
entry.getValue()
```

------------------------------------------------------------------------

## `filter()`

``` java
.filter(entry -> entry.getKey() != null && entry.getValue() != null)
```

Removes entries where either the key or value is `null`.

For example:

``` text
Baba=null
null=96
```

Both entries are removed.

------------------------------------------------------------------------

## `comparingByKey()`

Used to sort entries based on their keys.

### Ascending

``` java
.sorted(Map.Entry.comparingByKey())
```

### Descending

``` java
.sorted(Map.Entry.<String, Integer>comparingByKey().reversed())
```

------------------------------------------------------------------------

## `comparingByValue()`

Used to sort entries based on their values.

### Ascending

``` java
.sorted(Map.Entry.comparingByValue())
```

### Descending

``` java
.sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
```

------------------------------------------------------------------------

## Why `LinkedHashMap`?

`Collectors.toMap()` by itself does not guarantee that the sorted stream
order will be retained in the resulting map.

Therefore, we use:

``` java
LinkedHashMap::new
```

This preserves the encounter order.

------------------------------------------------------------------------

## Why `(a, b) -> a`?

This is the merge function required by this overload of
`Collectors.toMap()`:

``` java
Collectors.toMap(
    keyMapper,
    valueMapper,
    mergeFunction,
    mapSupplier
)
```

Here:

``` java
(a, b) -> a
```

means that if duplicate keys occur, keep the first value.

------------------------------------------------------------------------

# 4. Common Interview Questions

## Q1. How do you sort a Map by key in ascending order?

### Answer

``` java
map.entrySet()
   .stream()
   .sorted(Map.Entry.comparingByKey())
   .collect(Collectors.toMap(
       Map.Entry::getKey,
       Map.Entry::getValue,
       (a, b) -> a,
       LinkedHashMap::new
   ));
```

------------------------------------------------------------------------

## Q2. How do you sort a Map by key in descending order?

### Answer

Use `reversed()`:

``` java
.sorted(Map.Entry.<String, Integer>comparingByKey().reversed())
```

------------------------------------------------------------------------

## Q3. How do you sort a Map by value in ascending order?

### Answer

``` java
.sorted(Map.Entry.comparingByValue())
```

------------------------------------------------------------------------

## Q4. How do you sort a Map by value in descending order?

### Answer

``` java
.sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
```

------------------------------------------------------------------------

## Q5. Why can't we simply use `HashMap` after sorting?

### Answer

`HashMap` does not guarantee iteration order. If we want to preserve the
order generated by the sorted stream, `LinkedHashMap` is commonly used.

------------------------------------------------------------------------

## Q6. What is the difference between `HashMap` and `LinkedHashMap`?

  Feature                               HashMap                     LinkedHashMap
  ------------------------------------- --------------------------- --------------------------------------
  Maintains insertion/encounter order   No                          Yes
  Allows one null key                   Yes                         Yes
  Allows null values                    Yes                         Yes
  Performance                           Generally slightly faster   Slightly more overhead
  Use case                              Fast lookup                 Lookup + predictable iteration order

------------------------------------------------------------------------

## Q7. What happens if we don't filter null values before `comparingByValue()`?

`Map.Entry.comparingByValue()` expects comparable non-null values in the
normal case. A `null` value can cause a `NullPointerException` during
sorting.

Therefore, filtering null values first is a safe approach:

``` java
.filter(entry -> entry.getKey() != null && entry.getValue() != null)
```

------------------------------------------------------------------------

# 5. Programming Interview Questions

## Question 1: Sort a Map by Key in Descending Order

Given:

``` java
Map<String, Integer> map = new HashMap<>();

map.put("John", 20);
map.put("Alex", 70);
map.put("Mike", 90);
map.put("Bob", 10);
```

### Expected Output

``` text
{Mike=90, John=20, Bob=10, Alex=70}
```

### Solution

``` java
Map<String, Integer> result = map.entrySet()
        .stream()
        .sorted(Map.Entry.<String, Integer>comparingByKey().reversed())
        .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (a, b) -> a,
                LinkedHashMap::new
        ));

System.out.println(result);
```

------------------------------------------------------------------------

# 6. Programming Question 2: Sort by Value Descending

Given:

``` java
Map<String, Integer> map = new HashMap<>();

map.put("John", 20);
map.put("Alex", 70);
map.put("Mike", 90);
map.put("Bob", 10);
```

### Expected Output

``` text
{Mike=90, Alex=70, John=20, Bob=10}
```

### Solution

``` java
Map<String, Integer> result = map.entrySet()
        .stream()
        .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
        .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (a, b) -> a,
                LinkedHashMap::new
        ));

System.out.println(result);
```

------------------------------------------------------------------------

# 7. Programming Question 3: Remove Null Key and Null Values

Given:

``` java
Map<String, Integer> map = new HashMap<>();

map.put("A", 10);
map.put("B", null);
map.put(null, 20);
map.put("C", 30);
```

Remove all entries having either a null key or null value.

### Expected Output

``` text
{A=10, C=30}
```

### Solution

``` java
Map<String, Integer> result = map.entrySet()
        .stream()
        .filter(entry ->
                entry.getKey() != null &&
                entry.getValue() != null)
        .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue
        ));

System.out.println(result);
```

------------------------------------------------------------------------

# 8. Programming Question 4: Find the Maximum Value in a Map

Given:

``` java
Map<String, Integer> map = new HashMap<>();

map.put("A", 100);
map.put("B", 500);
map.put("C", 300);
map.put("D", 200);
```

Find the employee/product having the maximum value.

### Expected Output

``` text
B=500
```

### Solution

``` java
Map.Entry<String, Integer> result = map.entrySet()
        .stream()
        .max(Map.Entry.comparingByValue())
        .orElse(null);

System.out.println(result);
```

------------------------------------------------------------------------

# 9. Programming Question 5: Find the Minimum Value in a Map

### Solution

``` java
Map.Entry<String, Integer> result = map.entrySet()
        .stream()
        .min(Map.Entry.comparingByValue())
        .orElse(null);

System.out.println(result);
```

------------------------------------------------------------------------

# 10. Programming Question 6: Get Top 2 Entries by Value

Given:

``` java
Map<String, Integer> map = new HashMap<>();

map.put("A", 100);
map.put("B", 500);
map.put("C", 300);
map.put("D", 200);
```

### Expected Output

``` text
B=500
C=300
```

### Solution

``` java
map.entrySet()
        .stream()
        .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
        .limit(2)
        .forEach(System.out::println);
```

------------------------------------------------------------------------

# 11. Programming Question 7: Find Duplicate Values

Given:

``` java
Map<String, Integer> map = new HashMap<>();

map.put("A", 100);
map.put("B", 200);
map.put("C", 100);
map.put("D", 300);
map.put("E", 200);
```

Find values that occur more than once.

### Expected Output

``` text
100
200
```

### Possible Stream Solution

``` java
map.values()
        .stream()
        .collect(Collectors.groupingBy(
                value -> value,
                Collectors.counting()
        ))
        .entrySet()
        .stream()
        .filter(entry -> entry.getValue() > 1)
        .forEach(entry -> System.out.println(entry.getKey()));
```

------------------------------------------------------------------------

# 12. Programming Question 8: Sort by Value and Then by Key

If two employees have the same salary, sort those employees by name.

Example:

``` text
Raj=500
Aman=300
John=500
Mike=300
```

Expected:

``` text
Aman=300
Mike=300
John=500
Raj=500
```

### Solution

``` java
Map<String, Integer> result = map.entrySet()
        .stream()
        .sorted(
                Map.Entry.<String, Integer>comparingByValue()
                        .thenComparing(Map.Entry.comparingByKey())
        )
        .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (a, b) -> a,
                LinkedHashMap::new
        ));

System.out.println(result);
```

------------------------------------------------------------------------

# 13. Programming Question 9: Sort by Value Descending and Key Ascending

For example:

``` text
Raj=500
Aman=300
John=500
Mike=300
```

Expected:

``` text
John=500
Raj=500
Aman=300
Mike=300
```

### Solution

``` java
Map<String, Integer> result = map.entrySet()
        .stream()
        .sorted(
                Map.Entry.<String, Integer>comparingByValue()
                        .reversed()
                        .thenComparing(Map.Entry.comparingByKey())
        )
        .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (a, b) -> a,
                LinkedHashMap::new
        ));

System.out.println(result);
```

------------------------------------------------------------------------

# 14. Quick Interview Cheat Sheet

  Requirement         Code
  ------------------- -------------------------------------------
  Key ASC             `Map.Entry.comparingByKey()`
  Key DESC            `Map.Entry.comparingByKey().reversed()`
  Value ASC           `Map.Entry.comparingByValue()`
  Value DESC          `Map.Entry.comparingByValue().reversed()`
  Preserve order      `LinkedHashMap::new`
  Remove null key     `filter(e -> e.getKey() != null)`
  Remove null value   `filter(e -> e.getValue() != null)`
  Maximum value       `.max(Map.Entry.comparingByValue())`
  Minimum value       `.min(Map.Entry.comparingByValue())`
  Top N values        `.sorted(...reversed()).limit(N)`
  Secondary sorting   `.thenComparing(...)`

------------------------------------------------------------------------

# 15. Interview Challenge Questions

Try solving these without looking at the solution:

1.  Sort a `Map<String, Integer>` by key without using Java 8 Streams.
2.  Sort a map by value descending and return only the top 3 entries.
3.  Sort a map by value ascending; if values are equal, sort keys
    descending.
4.  Remove null keys and null values from a map.
5.  Find the key having the highest value.
6.  Find the key having the second-highest value.
7.  Find the top 3 employees based on salary.
8.  Find all duplicate values in a map.
9.  Count the frequency of values in a map.
10. Convert a `Map<String, Integer>` into a sorted `LinkedHashMap`.
11. Sort a map by key length.
12. Sort a map by key ignoring case.
13. Sort a `Map<String, List<Integer>>` based on the size of each list.
14. Sort employees by salary descending and name ascending when salary
    is equal.
15. Sort a map without modifying the original map.
16. Explain why `HashMap` cannot be relied upon to preserve sorted
    order.
17. Explain the purpose of the merge function `(a, b) -> a` in
    `Collectors.toMap()`.
18. Write the same sorting logic without Streams.
19. Handle null keys and null values while sorting safely.
20. Explain the difference between `Map.Entry.comparingByKey()` and
    `Map.Entry.comparingByValue()`.

------------------------------------------------------------------------

# 16. Most Important Interview Pattern

Remember this general pattern:

``` java
Map<String, Integer> result = map.entrySet()
        .stream()
        .sorted(
                Map.Entry.<String, Integer>comparingByValue()
                        .reversed()
        )
        .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (a, b) -> a,
                LinkedHashMap::new
        ));
```

The four important pieces are:

``` text
entrySet()
    ↓
stream()
    ↓
sorted(comparator)
    ↓
collect(toMap(... LinkedHashMap))
```

This pattern is frequently useful in Java 8 Stream coding interviews.
