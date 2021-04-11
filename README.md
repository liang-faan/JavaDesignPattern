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
Abstract Factory Pattern says that just **`define an interface or abstract class for creating families of related (or dependent) objects but without specifying their concrete sub-classes`**.That means Abstract Factory lets a class returns a factory of classes. So, this is the reason that Abstract Factory Pattern is one level higher than the Factory Pattern.
An Abstract Factory Pattern is also known as `Kit`.
#### Advantage of Abstract Factory Pattern
- Abstract Factory Pattern isolates the client code from concrete (implementation) classes.
- It eases the exchanging of object families.
- It promotes consistency among objects.
#### Usage of Abstract Factory Pattern
- When the system needs to be independent of how its object are created, composed, and represented.
- When the family of related objects has to be used together, then this constraint needs to be enforced.
- When you want to provide a library of objects that does not show implementations and only reveals interfaces.
- When the system needs to be configured with one of a multiple family of objects.
#### UML for Abstract Factory Pattern
- We are going to create a Bank interface and a Loan abstract class as well as their sub-classes.
- Then we will create AbstractFactory class as next step.
- Then after we will create concrete classes, BankFactory, and LoanFactory that will extends AbstractFactory class
- After that, AbstractFactoryPatternExample class uses the FactoryCreator to get an object of AbstractFactory class.
- See the diagram carefully which is given below:
![abstractfactory](/images/abstractfactory.jpg)
#### Example of Abstract Factory Pattern
Here, we are calculating the loan payment for different banks like HDFC, ICICI, SBI etc.
- Step 1: Create a Bank interface
```java
import java.io.*;     
interface Bank{  
        String getBankName();  
}
```
- Step 2: Create concrete classes that implement the Bank interface.
```java
class HDFC implements Bank{  
         private final String BNAME;  
         public HDFC(){  
                BNAME="HDFC BANK";  
        }  
        public String getBankName() {  
                  return BNAME;  
        }  
}

class ICICI implements Bank{  
       private final String BNAME;  
       ICICI(){  
                BNAME="ICICI BANK";  
        }  
        public String getBankName() {  
                  return BNAME;  
       }  
}  

class SBI implements Bank{  
      private final String BNAME;  
      public SBI(){  
                BNAME="SBI BANK";  
        }  
       public String getBankName(){  
                  return BNAME;  
       }  
}  
```
- Step 3: Create the Loan abstract class.
```java
abstract class Loan{  
   protected double rate;  
   abstract void getInterestRate(double rate);  
   public void calculateLoanPayment(double loanamount, int years)  
   {  
        /* 
              to calculate the monthly loan payment i.e. EMI   
                            
              rate=annual interest rate/12*100; 
              n=number of monthly installments;            
              1year=12 months. 
              so, n=years*12; 
 
            */  
                
         double EMI;  
         int n;  
  
         n=years*12;  
         rate=rate/1200;  
         EMI=((rate*Math.pow((1+rate),n))/((Math.pow((1+rate),n))-1))*loanamount;  
  
System.out.println("your monthly EMI is "+ EMI +" for the amount"+loanamount+" you have borrowed");     
 }  
}// end of the Loan abstract class.  
```
- Step 4: Create concrete classes that extend the Loan abstract class.
```java
class HomeLoan extends Loan{  
     public void getInterestRate(double r){  
         rate=r;  
    }  
}//End of the HomeLoan class.  


class BussinessLoan extends Loan{  
    public void getInterestRate(double r){  
          rate=r;  
     }  
  
}//End of the BusssinessLoan class.  

class EducationLoan extends Loan{  
     public void getInterestRate(double r){  
       rate=r;  
 }  
}//End of the EducationLoan class.  
```
- Step 5: Create an abstract class (i.e AbstractFactory) to get the factories for Bank and Loan Objects.
```java
abstract class AbstractFactory{  
  public abstract Bank getBank(String bank);  
  public abstract Loan getLoan(String loan);  
}
```
- Step 6: Create the factory classes that inherit AbstractFactory class to generate the object of concrete class based on given information.
```java
class BankFactory extends AbstractFactory{  
   public Bank getBank(String bank){  
      if(bank == null){  
         return null;  
      }  
      if(bank.equalsIgnoreCase("HDFC")){  
         return new HDFC();  
      } else if(bank.equalsIgnoreCase("ICICI")){  
         return new ICICI();  
      } else if(bank.equalsIgnoreCase("SBI")){  
         return new SBI();  
      }  
      return null;  
   }  
  public Loan getLoan(String loan) {  
      return null;  
   }  
}//End of the BankFactory class.  
```
```java
class LoanFactory extends AbstractFactory{  
           public Bank getBank(String bank){  
                return null;  
          }  
        
     public Loan getLoan(String loan){  
      if(loan == null){  
         return null;  
      }  
      if(loan.equalsIgnoreCase("Home")){  
         return new HomeLoan();  
      } else if(loan.equalsIgnoreCase("Business")){  
         return new BussinessLoan();  
      } else if(loan.equalsIgnoreCase("Education")){  
         return new EducationLoan();  
      }  
      return null;  
   }  
     
}  
```
- Step 7: Create a FactoryCreator class to get the factories by passing an information such as Bank or Loan.
```java
class FactoryCreator {  
     public static AbstractFactory getFactory(String choice){  
      if(choice.equalsIgnoreCase("Bank")){  
         return new BankFactory();  
      } else if(choice.equalsIgnoreCase("Loan")){  
         return new LoanFactory();  
      }  
      return null;  
   }  
}//End of the FactoryCreator.  
```
- Step 8: Use the FactoryCreator to get AbstractFactory in order to get factories of concrete classes by passing an information such as type.
```java
import java.io.*;  
class AbstractFactoryPatternExample {  
    public static void main(String args[])throws IOException {  
       
    BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
  
    System.out.print("Enter the name of Bank from where you want to take loan amount: ");  
    String bankName=br.readLine();  
  
    System.out.print("\n");  
    System.out.print("Enter the type of loan e.g. home loan or business loan or education loan : ");  
    
    String loanName=br.readLine();  
    AbstractFactory bankFactory = FactoryCreator.getFactory("Bank");  
    Bank b=bankFactory.getBank(bankName);  
    
    System.out.print("\n");  
    System.out.print("Enter the interest rate for "+b.getBankName()+ ": ");  
    
    double rate=Double.parseDouble(br.readLine());  
    System.out.print("\n");  
    System.out.print("Enter the loan amount you want to take: ");  
    
    double loanAmount=Double.parseDouble(br.readLine());  
    System.out.print("\n");  
    System.out.print("Enter the number of years to pay your entire loan amount: ");  
    int years=Integer.parseInt(br.readLine());  
    
    System.out.print("\n");  
    System.out.println("you are taking the loan from "+ b.getBankName());  
    
    AbstractFactory loanFactory = FactoryCreator.getFactory("Loan");  
            Loan l=loanFactory.getLoan(loanName);  
            l.getInterestRate(rate);  
            l.calculateLoanPayment(loanAmount,years);  
    }  
}//End of the  AbstractFactoryPatternExample   
```
- Ouput

![abstractfactory](/images/abstractfactoryoutput.jpg)

- [download this Abstract Factory Pattern Example](/src/abstractfactorypattern.zip)

### 1.3 Singleton Pattern
Singleton Pattern says that just **`define a class that has only one instance and provides a global point of access to it`**.

In other words, a class must ensure that only single instance should be created and single object can be used by all other classes.

There are two forms of singleton design pattern
- Early Instantiation: creation of instance at load time.
- Lazy Instantiation: creation of instance when required.
#### Advantage of Singleton design pattern
- Saves memory because object is not created at each request. Only single instance is reused again and again.
#### Usage of Singleton design pattern
- Singleton pattern is mostly used in multi-threaded and database applications. It is used in logging, caching, thread pools, configuration settings etc.
#### Uml of Singleton design pattern

![Singleton](images/singleton.jpg)

#### How to create Singleton design pattern?
To create the singleton class, we need to have static member of class, private constructor and static factory method.
- `Static member`: It gets memory only once because of static, itcontains the instance of the Singleton class.
- `Private constructor`: It will prevent to instantiate the Singleton class from outside the class.
- `Static factory method`: This provides the global point of access to the Singleton object and returns the instance to the caller.

#### Understanding early Instantiation of Singleton Pattern
In such case, we create the instance of the class at the time of declaring the static data member, so instance of the class is created at the time of classloading.

Let's see the example of singleton design pattern using early instantiation.

```java
class A{  
    private static A obj=new A();//Early, instance will be created at load time  
    private A(){}

    public static A getA(){  
    return obj;  
    }

    public void doSomething(){  
    //write your code  
    }
}
```
#### Understanding lazy Instantiation of Singleton Pattern
In such case, we create the instance of the class in synchronized method or synchronized block, so instance of the class is created when required.

Let's see the simple example of singleton design pattern using lazy instantiation.

```java
class A {
    private static volatile A obj;
    /*
    volatile make sure variable write to main memory
    if deploy environment has multiple CPU, each CPU will have its own cache. 
    To make sure all CPU refers to the same instance, volatile make sure variable ready from main memory. 
    */

    private A() {
    }

    public static A getA() {
        if (obj == null) {
            synchronized (A.class) {
                if (obj == null) {
                    obj = new A();//instance will be created at request time  
                }
            }
        }
        return obj;
    }

    public void doSomething() {
        //write your code  
    }
}
```
#### Significance of Classloader in Singleton Pattern
:book: If singleton class is loaded by two classloaders, two instance of singleton class will be created, one for each classloader.


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
