## SOLID PRINCIPLES
          1. Single Responsibility Principle (SRP)
          2. Open-Closed Principle (OCP)
          3. Liskov Substitution Principle (LSP)
          4. Interface Segregation Principle (ISP)
          5. Dependency Inversion Principle (DIP)

##  1. Single Responsibility Principle (SRP)
                    The single responsibility principle states that every Java class must perform a single functionality. Implementation of multiple functionalities in a single class mashup the code and if any modification is required may affect the whole class. It precise the code and the code can be easily maintained.
                    For Example The problem is all methods are in a single class:
                    Public class Student {
                    	public void printDetails() {
                    	}
                    
                    	public void calculatePercentage() {
                    	}
                    
                    	public void addStudent() {
                    	}
                    }
                    Solution: separate all methods into different classes:
                    public class Student {
                    	public void addStudent() {
                    	}
                    }
                    public class PrintStudentDetails {
                    	public void printDetails() {
                    	}
                    }
                    public class Percentage {
                    	public void calculatePercentage() {
                    	}
                    }

## 2. Open-Closed Principle (OCP)
                    The open-closed principle states that the module should be open for extension but closed for modification according to new requirements. The extension allows us to implement new functionality in the module.
                    For Example, All vehicles are defined as single-class. if I want to add another name like Truck, it will violate the open-closed principle.
                    public class VehicleInfo {
                    	public double vehicleNumber(Vehicle vcl) {
                    		if (vcl instanceof Car) {
                    			return vcl.getNumber();
                    		}
                    		if (vcl instanceof Bike) {
                    			return vcl.getNumber();
                    		}
                    	}
                    }
                    Solution, we can create one vehicle info class and extend it to other types of vehicles.
                    public class VehicleInfo {
                    	public double vehicleNumber() {
                    	}
                    }

                    public class Car extends VehicleInfo {
                    	public double vehicleNumber() {
                    		return this.getValue();
                    	}
                    }

                    public class Car extends Truck {
                    	public double vehicleNumber() {
                    		return this.getValue();
                    	}
                    }

## 3. Liskov Substitution Principle (LSP)
                     It applies to inheritance in such a way that the derived classes must be completely substitutable for their base classes. In other words, if class A is a subtype of class B, then we should be able to replace B with A without interrupting the behavior of the program.
                               @Data
                              public class Video{
                              	private String title;
                              	private int time;
                              	private int likes;
                              	private int views;
                              	
                              	public double getNumberOfHoursPlayed() {
                              		return (time/3600.0)*views;
                              	}
                              	public void playRandomAd() throws Exceptions{
                              		// play ad
                              		
                              	}
                              }
                              supose we have premium video and no Ad should play.
                              
                              public class PremiumVideo extends Video{
                              	private int premiumId;
                              	@override
                              	public void playRandomAd() throws Exceptions {
                              		throw new Exception("No Ad play during Premium vidoes");
                              	}
                              }
                              // this is not a good idea, this exception might be thrown causes application crash
                              
                              Soution is to refactor the code and create new class
                              
                              public class VideoManager {
                              	private String title;
                              	private int time;
                              	private int likes;
                              	private int views;public double getNumberOfHoursPlayed() {
                              		return (time/3600.0)*views;
                              	}
                              	public void playRandomAd() throws Exceptions{
                              		// Play Ads
                              		
                              	}
                              }
                              
                              Now use VideoManger methods into Video and PremiumVideo
                              
                              public class Video {
                              	private VideoManager manager;
                              	public double getNumberOfHoursPlayed() {
                              		return manager.getNumberOfHours();
                              	}
                              	public void playeRandomAd() {
                              		manager.playRandomAd();
                              	}
                              }
                              
                              public class PremiumVideo {
                              	private VideoManager manager;
                              	private int premiumId;
                              	
                              	public void playRandomAd() throws Exceptions {
                              		return manager.getNumberOfHours();
                              	}
                              }

 ## 4. Interface Segregation Principle (ISP):
           The principle states that the larger interfaces split into smaller ones. Because the implementation classes use only the methods that are required. We should not force the client to use the methods that they do not want to use.
           Example :
           public interface IVideoActions {
          	double getNumberOfHoursPlayed();
          	void playRandomAd();
          }
          
          @Data
          public class Video implements IVideoActions{
          	private String title;
          	private int time;
          	private int likes;
          	private int views;
          	@override
          	public double getNumberOfHoursPlayed() {
          		return (time/3600.0)*views;
          	}
          	@override
          	public void playRandomAd() throws Exceptions{
          		// play ad
          		
          	}
          }
          
          public class PremiumVideo implements IVideoActions{
          	private int premiumId;
          	@override
          	public double getNumberOfHoursPlayed() {
          		return (time/3600.0)*views;
          	}
          	@override
          	public void playRandomAd() throws Exceptions {
          		throw new Exception("No Ad play during Premium vidoes");
          	}
          }
          In this case, we have to override getNUmberOfHoursPlayed and playRandomAd(). which violates Liskov Substitution Principle.
          We can define 2 interfaces here.
          public interface IVideoActions {
          	double getNumberOfHoursPlayed();
          }
          
          public interface IAdActions {
          	void playRandomAd();
          }
          
          @Data
          public class Video implements IVideoActions, IAdActions{
          	private String title;
          	private int time;
          	private int likes;
          	private int views;
          	@override
          	public double getNumberOfHoursPlayed() {
          		return (time/3600.0)*views;
          	}
          	@override
          	public void playRandomAd() throws Exceptions{
          		// play ad
          		
          	}
          }
          
          
          public class PremiumVideo implements IAdActions{
          	private int premiumId;
          	public double getNumberOfHoursPlayed() {
          		return (time/3600.0)*views;
          	}
          }
          
##  5. Dependency Inversion Principle (DIP)
          The principle states that we must use abstraction (abstract classes and interfaces) instead of concrete implementations. High-level modules should not depend on the low-level module but both should depend on the abstraction. Because the abstraction does not depend on detail but the detail depends on abstraction. It decouples the software.
          
