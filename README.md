# Java Design Pattern
## 1. [Creational Design Pattern](#1-creational-design-pattern-1)
### 1.1 [Factory Pattern](#11-factory-pattern-1)
### 1.2 [Abstract Factory Pattern](#12-abstract-factory-pattern-1)
### 1.3 [Singleton Pattern](#13-singleton-pattern-1)
### 1.4 [Prototype Pattern](#14-prototype-pattern-1)
### 1.5 [Builder Pattern](#15-builder-pattern-1)
## 2. [Structural Design Pattern](#2-structural-design-pattern-1)
### 2.1 [Adapter Pattern](#21-adapter-pattern-1)
### 2.2 [Bridge Pattern](#22-bridge-pattern-1)
### 2.3 [Composite Pattern](#23-composite-pattern-1)
### 2.4 [Decorator Pattern](#24-decorator-pattern-1)
### 2.5 [Facade Pattern](#25-facade-pattern-1)
### 2.6 [Flyweight Pattern](#26-flyweight-pattern-1)
### 2.7 [Proxy Pattern](#27-proxy-pattern-1)
## 3. [Behavioral Design Pattern](#3-behavioral-design-pattern-1)
### 3.1 [Chain Of Responsibility Pattern](#31-chain-of-responsibility-pattern-1)
### 3.2 [Command Pattern](#32-command-pattern-1)
### 3.3 [Interpreter Pattern](#33-interpreter-pattern-1)
### 3.4 [Iterator Pattern](#34-iterator-pattern-1)
### 3.5 [Mediator Pattern](#35-mediator-pattern-1)
### 3.6 [Memento Pattern](#36-memento-pattern-1)
### 3.7 [Observer Pattern](#37-observer-pattern-1)
### 3.8 [State Pattern](#38-state-pattern-1)
### 3.9 [Strategy Pattern](#39-strategy-pattern-1)
### 3.10 [Template Pattern](#310-template-pattern-1)
### 3.11 [Visitor Pattern](#311-visitor-pattern-1)

## 1. Creational Design Pattern
Creational design patterns are concerned with the way of creating objects. These design patterns are used when a decision must be made at the time of instantiation of a class (i.e. creating an object of a class).

But everyone knows an object is created by using new keyword in java. For example:
```java
StudentRecord s1=new StudentRecord();  
```
Hard-Coded code is not the good programming approach. Here, we are creating the instance by using the new keyword. Sometimes, the nature of the object must be changed according to the nature of the program. In such cases, we must get the help of creational design patterns to provide more general and flexible approach.
### 1.1 Factory Pattern
A Factory Pattern or Factory Method Pattern says that just **`define an interface or abstract class for creating an object but let the subclasses decide which class to instantiate`**. In other words, subclasses are responsible to create the instance of the class.

The Factory Method Pattern is also known as **`Virtual Constructor`**.
#### Advantage of Factory Design Pattern
- Factory Method Pattern allows the sub-classes to choose the type of objects to create.
- It promotes the loose-coupling by eliminating the need to bind application-specific classes into the code. That means the code interacts solely with the resultant interface or abstract class, so that it will work with any classes that implement that interface or that extends that abstract class.
#### Usage of Factory Design Pattern
- When a class doesn't know what sub-classes will be required to create
- When a class wants that its sub-classes specify the objects to be created.
- When the parent classes choose the creation of objects to its sub-classes.
#### UML for Factory Method Pattern
- We are going to create a Plan abstract class and concrete classes that extends the Plan abstract class. A factory class GetPlanFactory is defined as a next step.
- GenerateBill class will use GetPlanFactory to get a Plan object. It will pass information (DOMESTICPLAN / COMMERCIALPLAN / INSTITUTIONALPLAN) to GetPalnFactory to get the type of object it needs.
![UML for Factory Method Pattern](/images/factorymethod.jpg)
#### Calculate Electricity Bill : A Real World Example of Factory Method
- Step 1: Create a Plan abstract class.
```java
import java.io.*;      
abstract class Plan{  
         protected double rate;  
         abstract void getRate();  
   
         public void calculateBill(int units){  
              System.out.println(units*rate);  
          }  
}//end of Plan class.
```
- Step 2: Create the concrete classes that extends Plan abstract class.
```java
class  DomesticPlan extends Plan{  
        //@override  
         public void getRate(){  
             rate=3.50;              
        }  
   }//end of DomesticPlan class.  

class  CommercialPlan extends Plan{  
   //@override   
    public void getRate(){   
        rate=7.50;  
   } //end of CommercialPlan class.  

class  InstitutionalPlan extends Plan{  
   //@override  
    public void getRate(){   
        rate=5.50;  
   } //end of InstitutionalPlan class.  
```
- Step 3: Create a GetPlanFactory to generate object of concrete classes based on given information.
```java
class GetPlanFactory{  
      
   //use getPlan method to get object of type Plan   
       public Plan getPlan(String planType){  
            if(planType == null){  
             return null;  
            }  
          if(planType.equalsIgnoreCase("DOMESTICPLAN")) {  
                 return new DomesticPlan();  
               }   
           else if(planType.equalsIgnoreCase("COMMERCIALPLAN")){  
                return new CommercialPlan();  
            }   
          else if(planType.equalsIgnoreCase("INSTITUTIONALPLAN")) {  
                return new InstitutionalPlan();  
          }  
      return null;  
   }  
}//end of GetPlanFactory class.  
```
- Step 4: Generate Bill by using the GetPlanFactory to get the object of concrete classes by passing an information such as type of plan DOMESTICPLAN or COMMERCIALPLAN or INSTITUTIONALPLAN.
```java
import java.io.*;    
class GenerateBill{  
    public static void main(String args[])throws IOException{  
      GetPlanFactory planFactory = new GetPlanFactory();  
        
      System.out.print("Enter the name of plan for which the bill will be generated: ");  
      BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
  
      String planName=br.readLine();  
      System.out.print("Enter the number of units for bill will be calculated: ");  
      int units=Integer.parseInt(br.readLine());  
  
      Plan p = planFactory.getPlan(planName);  
      //call getRate() method and calculateBill()method of DomesticPaln.  
  
       System.out.print("Bill amount for "+planName+" of  "+units+" units is: ");  
           p.getRate();  
           p.calculateBill(units);  
            }  
    }//end of GenerateBill class.  
```
- Output

    ![Sample Output](/images/factorymethodoutput.jpg)
    
- [Source Code Download](/src/factorymethodpattern.zip)
### 1.2 Abstract Factory Pattern
### 1.3 Singleton Pattern
### 1.4 Prototype Pattern
### 1.5 Builder Pattern

## 2. Structural Design Pattern
### 2.1 Adapter Pattern
### 2.2 Bridge Pattern
### 2.3 Composite Pattern
### 2.4 Decorator Pattern
### 2.5 Facade Pattern
### 2.6 Flyweight Pattern
### 2.7 Proxy Pattern

## 3. Behavioral Design Pattern
### 3.1 Chain Of Responsibility Pattern
### 3.2 Command Pattern
### 3.3 Interpreter Pattern
### 3.4 Iterator Pattern
### 3.5 Mediator Pattern
### 3.6 Memento Pattern
### 3.7 Observer Pattern
### 3.8 State Pattern
### 3.9 Strategy Pattern
### 3.10 Template Pattern
### 3.11 Visitor Pattern

#
*This file generated by [liang.faam](https://github.com/liang-faan/JavaDesignPattern) on April 11, 2021*

##
Resources reference to [Design Patterns in Java](https://www.javatpoint.com/design-patterns-in-java) @ javapoint.com
