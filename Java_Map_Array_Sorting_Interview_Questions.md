# Sort Array By Its Frequency
## Question 1

## What is the frequency of each element in the given array?

Input
int[] arr = {2,2,1,3,5,2,6,1,7,3,2,2,6,6,3,3};

Output
{2=5, 1=2, 3=4, 5=1, 6=3, 7=1}

## Question 2: Sort the array elements in ascending order based on their frequency using Map.

Output
[5, 7, 1, 1, 6, 6, 6, 3, 3, 3, 3, 2, 2, 2, 2, 2]

## Question 3: Sort the array elements in descending order based on their frequency using Map.

Output
[2, 2, 2, 2, 2, 3, 3, 3, 3, 6, 6, 6, 1, 1, 5, 7]

## Question 4: Sort the array elements in ascending order based on their frequency using a one-liner Stream solution.

Output
[5, 7, 1, 1, 6, 6, 6, 3, 3, 3, 3, 2, 2, 2, 2, 2]

## Question 5: Sort the array elements in descending order based on their frequency using a one-liner Stream solution.

Output
[2, 2, 2, 2, 2, 3, 3, 3, 3, 6, 6, 6, 1, 1, 5, 7]

	package Collections;
	
	import java.util.ArrayList;
	import java.util.Arrays;
	import java.util.LinkedHashMap;
	import java.util.List;
	import java.util.Map;
	import java.util.function.Function;
	import java.util.stream.Collectors;
	
	public class SortArrayByItsFrequency {
		public static void main(String[] args) {
			int[] arr= {2,2,1,3,5,2,6,1,7,3,2,2,6,6,3,3};
			// use Map
			Map<Integer,Integer> map=new LinkedHashMap<>();
			for(int i=0;i<arr.length;i++) {
				map.put(arr[i], map.getOrDefault(arr[i], 0)+1);
			}
			System.out.println(map);
			//Method-1 Print ascending order
			List<Integer> listASC=new ArrayList<>();
			map.entrySet().stream().sorted(Map.Entry.comparingByValue()).forEach(entry->
						{
							for(int i=0;i<entry.getValue();i++) {
								listASC.add(entry.getKey());
							}
						}
					);
			System.out.println(listASC);
		
		// Method-2 Print ascending order
		List<Integer> listDESC=new ArrayList<>();
		map.entrySet().stream().sorted(Map.Entry.<Integer,Integer>comparingByValue().reversed()).forEach(entry->
		{
			for(int i=0;i<entry.getValue();i++) {
				listDESC.add(entry.getKey());
			}
		});
		System.out.println(listDESC);
		
		//method-3 One liner solution ascending order
		List<Integer> listASCStore=new ArrayList<>();
		Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
		.entrySet().stream().sorted(Map.Entry.comparingByValue()).forEach(entry->
		{
			for(int i=0;i<entry.getValue();i++) {
				listASCStore.add(entry.getKey());
			}
		});
		System.out.println(listASCStore);
		
		//method-3 One liner solution ascending order
		List<Integer> listDESCStore=new ArrayList<>();
		Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(),LinkedHashMap::new, Collectors.counting())).entrySet().stream()
		.sorted(Map.Entry.<Integer,Long>comparingByValue().reversed()).forEach(entry->
		{
			for(int i=0;i<entry.getValue();i++) {
				listDESCStore.add(entry.getKey());
			}
		});
		System.out.println(listDESCStore);
	 }
	}

## 1. Find the frequency of each element in an integer array.
## 2. Find duplicate elements in an integer array.
## 3. Find unique elements in an integer array.
## 4. Find the first duplicate element in an integer array.
## 5. Find the first unique element in an integer array.
## 6. Find Max number from Array
## 7. Find 2nd Max number from Array
## 8. Find Min number from Array
## 9. Find 2nd Min number from Array

	package Collections;

	import java.util.Arrays;
	import java.util.Comparator;
	import java.util.LinkedHashMap;
	import java.util.function.Function;
	import java.util.stream.Collectors;
	
	public class ArrayManupulationsAnswerUsingMap {
		public static void main(String[] args) {
			int[] arr= {2,2,1,3,5,2,6,1,7,3,2,2,6,6,3,3};
			//Find the frequency of each element in an integer array.
			Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
			.forEach((k,v)->System.out.print(k+":"+v+" "));
			// question 1: Find duplicate elements in an integer array.
			System.out.println();
			Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
			.entrySet().stream().filter(entry->entry.getValue()>1).forEach(entry->System.out.print(entry.getKey()+" "));
			
			//Find unique elements in an integer array.
			System.out.println();
			Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
			.entrySet().stream().filter(entry->entry.getValue()==1).forEach(entry-> System.out.print(entry.getKey()+" "));
			
			//Find the first duplicate element in an integer array.
			System.out.println();
			Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
			.entrySet().stream().filter(entry->entry.getValue()>1).limit(1).forEach(entry->System.out.println(entry.getKey()));
			
			//Find the first unique element in an integer array.
			Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
					.entrySet().stream().filter(entry->entry.getValue()==1).limit(1).forEach(entry->System.out.println(entry.getKey()));
			
			// FInd Max number from Array
			Integer maxNumber=Arrays.stream(arr).distinct().boxed().sorted(Comparator.reverseOrder()).findFirst().get();
			System.out.println(maxNumber);
			
			// FInd 2nd Max number from Array
			Integer secondMax=Arrays.stream(arr).distinct().boxed().sorted(Comparator.reverseOrder()).skip(1).findFirst().get();
			System.out.println(secondMax);
			
			// FInd min number from Array
			Integer minNumber=Arrays.stream(arr).distinct().boxed().sorted().findFirst().get();
			System.out.println(minNumber);
			// FInd 2nd min number from Array
			Integer secondMin=Arrays.stream(arr).distinct().sorted().skip(1).findFirst().getAsInt();
			System.out.println(secondMin);
		 }
	}

## 1. Union of two Arrays
## 2. Intersection of two Arrays
## 3. Elements in array1 which are not in array2
## 4. Array2 Elements that are not in Array1

	package Collections;
	import java.util.LinkedHashSet;
	import java.util.Set;
	
	public class unionIntersectionArray {
		public static void main(String[] args) {
			int[] arr={1,8,4,7,6,2,5};
			int[] arr1={5,2,7,4,9};
			// Normal Method
			// Union of the 2 Arrays
			Set<Integer> unionElements= new LinkedHashSet<>();
			Set<Integer> intersctionElements= new LinkedHashSet<>();
			for(int i=0;i<arr.length;i++) {
				unionElements.add(arr[i]);
			}
			for(int i=0;i<arr1.length;i++) {
				unionElements.add(arr1[i]);
			}
			System.out.println("Union:"+unionElements);
			// Intersection of 2 Array
			unionElements.removeAll(unionElements);
			for(int i=0;i<arr.length;i++) {
				unionElements.add(arr[i]);
			}
			for(int i=0;i<arr1.length;i++) {
				if(unionElements.contains(arr1[i])) {
					intersctionElements.add(arr1[i]);
				}
			}
			System.out.println("Intersection: "+intersctionElements);
		
			// Elements in array1 which are not in array2
			unionElements.removeAll(intersctionElements);
			System.out.println("Array1 Elements that are not in Array2 "+unionElements);
			
			// Array2 Elements that are not in Array1
			unionElements.removeAll(unionElements);
			for(int i=0;i<arr1.length;i++) {
				unionElements.add(arr1[i]);
			}
			unionElements.removeAll(intersctionElements);
			System.out.println("Array2 Elements that are not in Array1 "+unionElements);
			
		}
	}
