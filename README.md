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

## WAP to count words and characters
        package StringReverseProblems;
        
        import java.util.Arrays;
        import java.util.function.Function;
        import java.util.stream.Collectors;
        
        public class CountWordsAndCharacters {
        	public static void main(String[] args) {
        		//count words
        		String str="this hi My name is sanjeet kumar pandit hey who is this mine";
        		Arrays.asList(str.split(" ")).stream().filter(space->!space.contains(" ")).collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
        		.forEach((k,v)->System.out.println(k+" "+v));
        		
        		// count chars
        		Arrays.asList(str.split("")).stream().filter(space->!space.contains(" ")).collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
        		.forEach((k,v)->System.out.println(k+" "+v));
        	}
        }

## WAP to reverse the string but preserve the space
              package StringReverseProblems;
              
              public class ReverseStringWithPreserveSpace {
              	public static void main(String[] args) {
              		String str = "sanjeet kumar pandit";
              		ReverseStringWithPreserveSpace reserve = new ReverseStringWithPreserveSpace();
              		reserve.preserveSpace(str);
              	}
              
              	private void preserveSpace(String str) {
              		int start = 0;
              		int end = str.length() - 1;
              		char[] ch = str.toCharArray();
              		while (start < end) {
              			if (ch[start] == ' ') {
              				start++;
              				continue;
              			} else if (ch[end] == ' ') {
              				end--;
              				continue;
              			} else {
              				char temp = ch[start];
              				ch[start] = ch[end];
              				ch[end] = temp;
              				start++;
              				end--;
              			}
              		}
              		System.out.println(String.valueOf(ch));
              	}
              }

## WAP to extract date from alphanumeric String.
          package StringReverseProblems;
          
          import java.util.regex.Matcher;
          import java.util.regex.Pattern;
          
          public class exractDateFromAlphanumeric {
          	public static void main(String[] args) {
          		String str="aldmwkldqe2022ksadmkad2022-10-02mdmndeww";
          		String datFormat="\\d{4}-\\d{2}-\\d{2}";
          		Pattern patt=Pattern.compile(datFormat);
          		Matcher mat=patt.matcher(str);
          		while(mat.find()) {
          			System.out.println(mat.group());
          		}
          	}
          }

## WAP to sort by lowercase, uppercase and numbers for example Input: cD87baAC23B and output : abcABC2378
                                package StringReverseProblems;
                                import java.util.ArrayList;
                                import java.util.Collections;
                                import java.util.List;
                                public class SortStringByLowerUpparCases {
                                	public static void main(String[] args) {
                                		String str="12AacC423AbDbdB";
                                		SortStringByLowerUpparCases sorting=new SortStringByLowerUpparCases();
                                		sorting.SortByCases(str);
                                	}
                                
                                	private void SortByCases(String str) {
                                		List<String> lowerCase=new ArrayList<>();
                                		List<String> upparCase=new ArrayList<>();
                                		List<String> numbers=new ArrayList<>();
                                		char[] ch=str.toCharArray();
                                		for(char c:ch) {
                                			if(Character.isLowerCase(c)) {
                                				lowerCase.add(String.valueOf(c));
                                			} else if(Character.isUpperCase(c)) {
                                				upparCase.add(String.valueOf(c));
                                			} else if(Character.isDigit(c)){
                                				numbers.add(String.valueOf(c));
                                			}
                                		}
                                		Collections.sort(lowerCase);
                                		Collections.sort(upparCase);
                                		Collections.sort(numbers);
                                		lowerCase.addAll(upparCase);
                                		lowerCase.addAll(numbers);
                                		System.out.println(lowerCase);
                                		
                                	}
                                }


## WAP to add 1 to a number represented in the array. Ex1 :{1,1,2} -> {1,1,3}, {1,2,9} -> {1,3,0}, {9,9,9} -> {1,0,0,0}
                                  package StringReverseProblems;
                                  import java.util.Arrays;
                                  public class AddOneInArrays {
                                  	public static void main(String[] args) {
                                  		int[] arr=new int[] {9,9,9};
                                  		AddOneInArrays obj=new AddOneInArrays();
                                  		obj.AddOne(arr);
                                  	}
                                  
                                  	private void AddOne(int[] arr) {
                                  		StringBuffer sb=new StringBuffer();
                                  		for(int i=0;i<arr.length;i++) {
                                  			sb.append(arr[i]);
                                  		}
                                  		System.out.println(sb);
                                  		int sum = Integer.parseInt(sb.toString())+1;
                                  		String[] num = String.valueOf(sum).split("");
                                  		System.out.println(Arrays.deepToString(num));
                                  	}
                                  }

## Longest Common Prefix
                                        package StringReverseProblems;
                                        
                                        public class LongestCommonPrefix {
                                        	public static void main(String[] args) {
                                        		String[] str = { "apple", "ape", "april" };
                                        		LongestCommonPrefix LongestCommonPrefix = new LongestCommonPrefix();
                                        
                                        		System.out.println(LongestCommonPrefix.LongestCommonPrefixString(str));
                                        	}
                                        
                                        	private String LongestCommonPrefixString(String[] str) {
                                        		if (str == null || str.length == 0) {
                                        			return "";
                                        		}
                                        		String pre = str[0];
                                        		for (int i = 0; i < str.length; i++) {
                                        			while (str[i].indexOf(pre) != 0) {
                                        				pre = pre.substring(0, str.length - 1);
                                        				if (pre.isEmpty()) {
                                        					return "";
                                        				}
                                        			}
                                        		}
                                        		return pre;
                                        	}
                                        }

## Find the minimum distance between the given two words

                                                  package StringReverseProblems;
                                                  
                                                  public class ShortedDistanceBetweenWords {
                                                  	public static void main(String[] args) {
                                                  		String[] str = { "the", "quick", "brown", "fox", "quick" };
                                                  		String word1 = "the";
                                                  		String word2 = "fox";
                                                  		ShortedDistanceBetweenWords obj = new ShortedDistanceBetweenWords();
                                                  		obj.shorteddistanceBetweenTwoWords(str, word1, word2);
                                                  	}
                                                  
                                                  	private void shorteddistanceBetweenTwoWords(String[] str, String word1, String word2) {
                                                  		int d1 = -1, d2 = -1;
                                                  		int minValue = Integer.MAX_VALUE;
                                                  		for (int i = 0; i < str.length; i++) {
                                                  			if (str[i] == word1) {
                                                  				d1 = i;
                                                  			}
                                                  			if (str[i] == word2) {
                                                  				d2 = i;
                                                  			}
                                                  			if (d1 != -1 && d2 != -1) {
                                                  				minValue = Math.min(minValue, Math.abs(d1 - d2));
                                                  			}
                                                  		}
                                                  		System.out.println(minValue);
                                                  	}
                                                  }
## WAP to print missing numbers for Example input:{1,5,2,4}, output: {0,2}
                    package StringReverseProblems;
                    public class FindMissingNumber {
                    	public static void main(String[] args) {
                    		int[] arr=new int[] {4,3,1,5};
                    		FindMissingNumber obj=new FindMissingNumber();
                    		obj.getMissingNumber(arr);
                    	}
                    
                    	private void getMissingNumber(int[] arr) {
                    		int[] hash = new int[arr.length+1];
                    		for(int i=0;i<arr.length-1;i++) {
                    			hash[arr[i]]++;
                    		}
                    		//System.out.println(Arrays.toString(arr));
                    		for(int i=0;i<=arr.length;i++) {
                    			if(hash[i]==0) {
                    				System.out.println(i);
                    			}
                    		}
                    	}
                    }

## WAP to merge to array arr1 = { 1, 3, 5, 7, 9 }, arr2 = { 2, 4, 6, 8 }, output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
                    import java.util.ArrayList;
                    import java.util.Collections;
                    import java.util.List;
                    
                    public class MergeTwoArray {
                    	public static void main(String[] args) {
                    		int[] arr1 = new int[] { 1, 3, 5, 7, 9 };
                    		int[] arr2 = new int[] { 2, 4, 6, 8 };
                    		MergeTwoArray mergeTwoArray = new MergeTwoArray();
                    		mergeTwoArray.MergeArray(arr1, arr2);
                    	}
                    
                    	private void MergeArray(int[] arr1, int[] arr2) {
                    		List<Integer> merge = new ArrayList<>();
                    		for (int i = 0; i < arr1.length; i++) {
                    			merge.add(arr1[i]);
                    		}
                    		for (int i = 0; i < arr2.length; i++) {
                    			merge.add(arr2[i]);
                    		}
                    		// 1. sorting it
                    		Collections.sort(merge);
                    		System.out.print(merge);
                    	}
                    }

  
## WAP to print product of numbers in array except for self input arr={1,2,3,4}, output:{24,12,8,6}
                package StringReverseProblems;
                
                import java.util.Arrays;
                
                public class PrintProductOfNumberExceptSelf {
                	public static void main(String[] args) {
                		int[] arr = { 1, 2, 3, 4 };
                		PrintProductOfNumberExceptSelf pr = new PrintProductOfNumberExceptSelf();
                		pr.ProductOfSelf(arr);
                	}
                
                	private void ProductOfSelf(int[] arr) {
                		int n = arr.length;
                		int[] left_product = new int[n]; // arr[1,1,2,6]
                		int[] right_product = new int[n]; // arr[24,12,4,1]
                		int[] output_product = new int[n]; // output_product =[24, 12, 8, 6]
                		left_product[0] = 1;
                		right_product[n - 1] = 1;
                		for (int i = 1; i < n; i++) {
                			left_product[i] = arr[i - 1] * left_product[i - 1];
                		}
                		for (int i = n - 2; i >= 0; i--) {
                			right_product[i]=arr[i+1]*right_product[i+1];
                		}
                		for(int i=0;i<n;i++) {
                			output_product[i]=left_product[i]*right_product[i];
                		}
                		System.out.println(Arrays.toString(output_product));
                	}
                }
