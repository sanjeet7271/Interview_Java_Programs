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
