# Java 8 Programs:
## 1.) Write a Java Program to print each character using Java 8
                import java.util.Map;
                import java.util.function.Function;
                import java.util.stream.Collectors;
                import java.util.stream.IntStream;

                public class CountWords {
                  public static void main(String[] args) {
                    String words="Java Learning tutorials";
                    Map<String, Long> countChars=IntStream.range(0, words.length()).mapToObj(i- >words.substring(i,i+1)).filter(i>!i.trim().isEmpty()).collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
                    System.out.println(countChars);
                  }
                }

## 2.) Write a java Program to sort frequency wise
            import java.util.ArrayList;
            import java.util.Collections;
            import java.util.LinkedHashMap;
            import java.util.Map;

            public class SortFrequencyWise2 {
              public static void main(String[] args) {
                SortFrequencyWise2 wise = new SortFrequencyWise2();
                int[] arr = { 7, 1, 3, 4, 7, 1, 7, 1, 4, 5, 1, 9, 3 };
                wise.sortArrayByFrequency(arr);
              }

              private void sortArrayByFrequency(int[] arr) {
                Map<Integer, Integer> map = new LinkedHashMap<>();
                for (int i = 0; i < arr.length; i++) {
                  map.put(arr[i], map.containsKey(arr[i]) ? map.get(arr[i]) + 1 : 1);
                }
                ArrayList<Integer> list = new ArrayList<>();
                map.entrySet().stream().sorted(Collections.reverseOrder(Map.Entry.comparingByValue())).forEach(entry -> {
                  for (int i = 0; i < entry.getValue(); i++) {
                    list.add(entry.getKey());
                  }
                });
                System.out.println(list);
              }
            }
