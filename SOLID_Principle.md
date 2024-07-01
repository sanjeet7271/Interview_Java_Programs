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
