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
## 3.) Write a Java Programs to print Numbers and Characters
              import java.util.regex.Matcher;
              import java.util.regex.Pattern;
              
              public class ExtractNumbers {
              	public static void main(String[] args) {
              
                  //1. Method using replcaAll method
              		  String str="A123Bhvghy56fgt"; 
              		  String digit=str.replaceAll("[a-zA-Z]", "");
              		  System.out.println(digit);
              		 
              		
              		//2. method Normal Java methods 
              		str="A123Bhvghy56fgt";
              		char[] ch=str.toCharArray();
              		StringBuffer num=new StringBuffer();
              		StringBuffer alp=new StringBuffer();
              		for(int i=0;i<ch.length;i++) {
              			if(Character.isDigit(ch[i])){
              				num.append(ch[i]);
              			}else if(Character.isAlphabetic(ch[i])) {
              				alp.append(ch[i]);
              			}
              		}
              		System.out.println("numbers :"+num);
              		System.out.println("Alphabets :"+alp);
              		
              		// 3. Method using pattern matching
              		Pattern p=Pattern.compile("\\d+");
              		Matcher match=p.matcher(str);
              		while(match.find()) {
              			System.out.println(match.group());
              		}
              		
              	}
              
              }

## 4. WAP to Print only duplicate and unique element
                      import java.util.Arrays;
                      import java.util.HashSet;
                      import java.util.List;
                      import java.util.Set;
                      import java.util.stream.Collectors;
                      
                      public class ExtractOnlyDuplicateNumbers {
                      	public static void main(String[] args) {
                      		//1. Method - Using normal Array
                      		int[] arr= {23,21,42,40,12,21,60,42,10,15,25};
                      		Set<Integer> set=new HashSet<>();
                      		List<Integer> duplicate=Arrays.stream(arr).boxed().filter(num->!set.add(num)).collect(Collectors.toList());
                      		System.out.println(duplicate);
                      		
                      		//2. Method: using list
                      		List<Integer> list=Arrays.asList(23,21,42,40,12,21,60,42,10,15,25);
                      		Set<Integer> set1=new HashSet<>();
                      		List<Integer> duplicateElement=list.stream().filter(e->!set1.add(e)).collect(Collectors.toList());
                      		System.out.println(duplicateElement);
                      		System.out.println("Unique element :"+set1);
                      	}
                      }

## WAP to print duplicate and unique words

                  import java.util.Arrays;
                  import java.util.HashSet;
                  import java.util.List;
                  import java.util.Set;
                  import java.util.stream.Collectors;
                  
                  public class ExtractOnlyDuplicateNumbers {
                  	public static void main(String[] args) {
                  		//1. Method - Using normal Array
                  		int[] arr= {23,21,42,40,12,21,60,42,10,15,25};
                  		Set<Integer> set=new HashSet<>();
                  		List<Integer> duplicate=Arrays.stream(arr).boxed().filter(num->!set.add(num)).collect(Collectors.toList());
                  		System.out.println(duplicate);
                  		
                  		//2. Method: using list
                  		List<Integer> list=Arrays.asList(23,21,42,40,12,21,60,42,10,15,25);
                  		Set<Integer> set1=new HashSet<>();
                  		List<Integer> duplicateElement=list.stream().filter(e->!set1.add(e)).collect(Collectors.toList());
                  		System.out.println(duplicateElement);
                  		System.out.println("Unique element :"+set1);
                  
                  	}
                  }

## WAP tp check password is strong
          package StringReverseProblems;

          import java.util.Arrays;
          import java.util.HashSet;
          import java.util.List;
          import java.util.Set;
          
          public class CheckPasswordStrong {
          	public static void main(String[] args) {
          		CheckPasswordStrong strong = new CheckPasswordStrong();
          		String str = "R@njeet#72872";
          		boolean isStrong = strong.checkStrongPassword(str);
          		if (isStrong) {
          			System.out.println("password is Strong");
          		} else {
          			System.out.println("password is not strong");
          		}
          	}
          
          	private boolean checkStrongPassword(String str) {
          		boolean hasLowerCase = false;
          		boolean hasUpparCase = false;
          		boolean hasDigit = false;
          		boolean hasSpecialChar = false;
          		boolean temp = false;
          		Set<Character> list = new HashSet<Character>(
          				Arrays.asList('!', '@', '#', '$', '%', '^', '&', '*', '(', ')', '-', '+'));
          		for (char ch : str.toCharArray()) {
          			if (Character.isLowerCase(ch)) {
          				hasLowerCase = true;
          			}
          			if (Character.isUpperCase(ch)) {
          				hasUpparCase = true;
          			}
          			if (Character.isDigit(ch)) {
          				hasDigit = true;
          			}
          			if (list.contains(ch)) {
          				hasSpecialChar = true;
          			}
          		}
          		if (hasLowerCase && hasUpparCase && hasDigit && hasSpecialChar && (str.length() >= 8)) {
          			temp = true;
          		} else {
          			temp = false;
          		}
          		return temp;
          	}
          }

## Convert into Binary from 1 to 10 range
            package StringReverseProblems;
            
            import java.util.List;
            import java.util.stream.Collectors;
            import java.util.stream.IntStream;
            
            public class ConvertIntoBinary {
            	public static void main(String[] args) {
            		//Method 1. print using for each
            		IntStream.range(1, 10).mapToObj(num->Integer.toBinaryString(num)).forEach(System.out::println);
            		//Method 2. collect into list and print it
            		List<String> listOfBinary=IntStream.range(1, 10).mapToObj(num->Integer.toBinaryString(num)).collect(Collectors.toList());
            		System.out.println(listOfBinary);
            	}
            }
