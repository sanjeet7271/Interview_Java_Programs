# Sort Array By Its Frequency
## Question 1

## What is the frequency of each element in the given array?

Input
int[] arr = {2,2,1,3,5,2,6,1,7,3,2,2,6,6,3,3};

Output
{2=5, 1=2, 3=4, 5=1, 6=3, 7=1}

## Question 2

## Sort the array elements in ascending order based on their frequency using Map.

Output
[5, 7, 1, 1, 6, 6, 6, 3, 3, 3, 3, 2, 2, 2, 2, 2]

## Question 3

## Sort the array elements in descending order based on their frequency using Map.

Output
[2, 2, 2, 2, 2, 3, 3, 3, 3, 6, 6, 6, 1, 1, 5, 7]

## Question 4

## Sort the array elements in ascending order based on their frequency using a one-liner Stream solution.

Output
[5, 7, 1, 1, 6, 6, 6, 3, 3, 3, 3, 2, 2, 2, 2, 2]

## Question 5

## Sort the array elements in descending order based on their frequency using a one-liner Stream solution.

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
