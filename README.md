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
:book: `If singleton class is loaded by two classloaders, two instance of singleton class will be created, one for each classloader.`

#### Significance of Serialization in Singleton Pattern

If singleton class is Serializable, you can serialize the singleton instance. Once it is serialized, you can deserialize it but it will not return the singleton object.

To resolve this issue, you need to override the readResolve() method that enforces the singleton. It is called just after the object is deserialized. It returns the singleton object.

```java
public class A implements Serializable {
    //your code of singleton  
    protected Object readResolve() {
        return getA();
    }

}
```

#### Understanding Real Example of Singleton Pattern
- We are going to create a JDBCSingleton class. This JDBCSingleton class contains its constructor as private and a private static instance jdbc of itself.
- JDBCSingleton class provides a static method to get its static instance to the outside world. Now, JDBCSingletonDemo class will use JDBCSingleton class to get the JDBCSingleton object.
![singletonexample](images/singletonexample.jpg)

`Assumption`: you have created a table userdata that has three fields uid, uname and upassword in mysql database. Database name is ashwinirajput, username is root, password is ashwini.

*`File: JDBCSingleton.java`*
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

class JDBCSingleton {
    //Step 1  
    // create a JDBCSingleton class.  
    //static member holds only one instance of the JDBCSingleton class.  

    private static JDBCSingleton jdbc;

    //JDBCSingleton prevents the instantiation from any other class.  
    private JDBCSingleton() {
    }

    //Now we are providing gloabal point of access.  
    public static JDBCSingleton getInstance() {
        if (jdbc == null) {
            jdbc = new JDBCSingleton();
        }
        return jdbc;
    }

    // to get the connection from methods like insert, view etc.   
    private static Connection getConnection() throws ClassNotFoundException, SQLException {

        Connection con = null;
        Class.forName("com.mysql.jdbc.Driver");
        con = DriverManager.getConnection("jdbc:mysql://localhost:3306/ashwanirajput", "root", "ashwani");
        return con;

    }

    //to insert the record into the database   
    public int insert(String name, String pass) throws SQLException {
        Connection c = null;

        PreparedStatement ps = null;

        int recordCounter = 0;

        try {

            c = this.getConnection();
            ps = c.prepareStatement("insert into userdata(uname,upassword)values(?,?)");
            ps.setString(1, name);
            ps.setString(2, pass);
            recordCounter = ps.executeUpdate();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (ps != null) {
                ps.close();
            }
            if (c != null) {
                c.close();
            }
        }
        return recordCounter;
    }

    //to view the data from the database        
    public void view(String name) throws SQLException {
        Connection con = null;
        PreparedStatement ps = null;
        ResultSet rs = null;

        try {

            con = this.getConnection();
            ps = con.prepareStatement("select * from userdata where uname=?");
            ps.setString(1, name);
            rs = ps.executeQuery();
            while (rs.next()) {
                System.out.println("Name= " + rs.getString(2) + "\t" + "Paasword= " + rs.getString(3));

            }

        } catch (Exception e) {
            System.out.println(e);
        } finally {
            if (rs != null) {
                rs.close();
            }
            if (ps != null) {
                ps.close();
            }
            if (con != null) {
                con.close();
            }
        }
    }

    // to update the password for the given username  
    public int update(String name, String password) throws SQLException {
        Connection c = null;
        PreparedStatement ps = null;

        int recordCounter = 0;
        try {
            c = this.getConnection();
            ps = c.prepareStatement(" update userdata set upassword=? where uname='" + name + "' ");
            ps.setString(1, password);
            recordCounter = ps.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {

            if (ps != null) {
                ps.close();
            }
            if (c != null) {
                c.close();
            }
        }
        return recordCounter;
    }

    // to delete the data from the database   
    public int delete(int userid) throws SQLException {
        Connection c = null;
        PreparedStatement ps = null;
        int recordCounter = 0;
        try {
            c = this.getConnection();
            ps = c.prepareStatement(" delete from userdata where uid='" + userid + "' ");
            recordCounter = ps.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (ps != null) {
                ps.close();
            }
            if (c != null) {
                c.close();
            }
        }
        return recordCounter;
    }
}// End of JDBCSingleton class  
```

*`File: JDBCSingletonDemo.java`*
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

class JDBCSingletonDemo {
    static int count = 1;
    static int choice;

    public static void main(String[] args) throws IOException {

        JDBCSingleton jdbc = JDBCSingleton.getInstance();


        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        do {
            System.out.println("DATABASE OPERATIONS");
            System.out.println(" --------------------- ");
            System.out.println(" 1. Insertion ");
            System.out.println(" 2. View      ");
            System.out.println(" 3. Delete    ");
            System.out.println(" 4. Update    ");
            System.out.println(" 5. Exit      ");

            System.out.print("\n");
            System.out.print("Please enter the choice what you want to perform in the database: ");

            choice = Integer.parseInt(br.readLine());
            switch (choice) {

                case 1: {
                    System.out.print("Enter the username you want to insert data into the database: ");
                    String username = br.readLine();
                    System.out.print("Enter the password you want to insert data into the database: ");
                    String password = br.readLine();

                    try {
                        int i = jdbc.insert(username, password);
                        if (i > 0) {
                            System.out.println((count++) + " Data has been inserted successfully");
                        } else {
                            System.out.println("Data has not been inserted ");
                        }

                    } catch (Exception e) {
                        System.out.println(e);
                    }

                    System.out.println("Press Enter key to continue...");
                    System.in.read();

                }//End of case 1  
                break;
                case 2: {
                    System.out.print("Enter the username : ");
                    String username = br.readLine();

                    try {
                        jdbc.view(username);
                    } catch (Exception e) {
                        System.out.println(e);
                    }
                    System.out.println("Press Enter key to continue...");
                    System.in.read();

                }//End of case 2  
                break;
                case 3: {
                    System.out.print("Enter the userid,  you want to delete: ");
                    int userid = Integer.parseInt(br.readLine());

                    try {
                        int i = jdbc.delete(userid);
                        if (i > 0) {
                            System.out.println((count++) + " Data has been deleted successfully");
                        } else {
                            System.out.println("Data has not been deleted");
                        }

                    } catch (Exception e) {
                        System.out.println(e);
                    }
                    System.out.println("Press Enter key to continue...");
                    System.in.read();

                }//End of case 3  
                break;
                case 4: {
                    System.out.print("Enter the username,  you want to update: ");
                    String username = br.readLine();
                    System.out.print("Enter the new password ");
                    String password = br.readLine();

                    try {
                        int i = jdbc.update(username, password);
                        if (i > 0) {
                            System.out.println((count++) + " Data has been updated successfully");
                        }

                    } catch (Exception e) {
                        System.out.println(e);
                    }
                    System.out.println("Press Enter key to continue...");
                    System.in.read();

                }// end of case 4  
                break;

                default:
                    return;
            }

        } while (choice != 4);
    }
}  
```

- [download this Singleton Pattern Example](/src/singleton.zip)
- Ouput

![Ouput 1](images/singletonoutput1.jpg)

![Ouput 2](images/singletonoutput2.jpg)

![Ouput 3](images/singletonoutput2.jpg)

### 1.4 Prototype Pattern
Prototype Pattern says that cloning of an existing object instead of creating new one and can also be customized as per the requirement.

This pattern should be followed, if the cost of creating a new object is expensive and resource intensive.

#### Advantage of Prototype Pattern

The main advantages of prototype pattern are as follows:
- It reduces the need of sub-classing.
- It hides complexities of creating objects.
- The clients can get new objects without knowing which type of object it will be.
- It lets you add or remove objects at runtime.

#### Usage of Prototype Pattern
- When the classes are instantiated at runtime.
- When the cost of creating an object is expensive or complicated.
- When you want to keep the number of classes in an application minimum.
- When the client application needs to be unaware of object creation and representation.

#### UML for Prototype Pattern

![prototype](images/prototype.jpg)

- We are going to create an interface *Prototype* that contains a method *getClone()* of *Prototype* type.
- Then, we create a concrete class *EmployeeRecord* which implements *Prototype* interface that does the cloning of *EmployeeRecord* object.
- *PrototypeDemo* class will uses this concrete class *EmployeeRecord*.

#### Example of Prototype Design Pattern

Let's see the example of prototype design pattern.

*File: Prototype.java*
```java
interface Prototype {  
  
     public Prototype getClone();  
      
}//End of Prototype interface.  
```
*File: EmployeeRecord.java*
```java
class EmployeeRecord implements Prototype {

    private int id;
    private String name, designation;
    private double salary;
    private String address;

    public EmployeeRecord() {
        System.out.println("   Employee Records of Oracle Corporation ");
        System.out.println("---------------------------------------------");
        System.out.println("Eid" + "\t" + "Ename" + "\t" + "Edesignation" + "\t" + "Esalary" + "\t\t" + "Eaddress");

    }

    public EmployeeRecord(int id, String name, String designation, double salary, String address) {

        this();
        this.id = id;
        this.name = name;
        this.designation = designation;
        this.salary = salary;
        this.address = address;
    }

    public void showRecord() {

        System.out.println(id + "\t" + name + "\t" + designation + "\t" + salary + "\t" + address);
    }

    @Override
    public Prototype getClone() {

        return new EmployeeRecord(id, name, designation, salary, address);
    }
}//End of EmployeeRecord class. 
```

*File: PrototypeDemo.java*
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

class PrototypeDemo {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.print("Enter Employee Id: ");
        int eid = Integer.parseInt(br.readLine());
        System.out.print("\n");

        System.out.print("Enter Employee Name: ");
        String ename = br.readLine();
        System.out.print("\n");

        System.out.print("Enter Employee Designation: ");
        String edesignation = br.readLine();
        System.out.print("\n");

        System.out.print("Enter Employee Address: ");
        String eaddress = br.readLine();
        System.out.print("\n");

        System.out.print("Enter Employee Salary: ");
        double esalary = Double.parseDouble(br.readLine());
        System.out.print("\n");

        EmployeeRecord e1 = new EmployeeRecord(eid, ename, edesignation, esalary, eaddress);

        e1.showRecord();
        System.out.println("\n");
        EmployeeRecord e2 = (EmployeeRecord) e1.getClone();
        e2.showRecord();
    }
}//End of the ProtoypeDemo class.  
```
- [download this Prototype Pattern Example](src/PrototypePattern.zip)
- Output

![prototypeoutput](images/prototypeoutput.jpg)

### 1.5 Builder Pattern
Builder Pattern says that **`construct a complex object from simple objects using step-by-step approach`**

It is mostly used when object can't be created in single step like in the de-serialization of a complex object.

#### Advantage of Builder Design Pattern

The main advantages of Builder Pattern are as follows:

- It provides clear separation between the construction and representation of an object.
- It provides better control over construction process.
- It supports to change the internal representation of objects.

#### UML for Builder Pattern Example

![Builder Pattern Example](images/builderuml1.jpg)

#### Example of Builder Design Pattern
To create simple example of builder design pattern, you need to follow 6 following steps.

- 1) [Create Packing interface](#create-packing-interface)
- 2) Create 2 abstract classes CD and Company
- 3) Create 2 implementation classes of Company: Sony and Samsung
- 4) Create the CDType class
- 5)  Create the CDBuilder class
- 6)  Create the BuilderDemo class

##### 1) Create Packing interface
*File: Packing.java*
```java
public interface Packing {
    public String pack();

    public int price();
} 
```
##### 2) Create 2 abstract classes CD and Company
Create an abstract class CD which will implement Packing interface.
*File: CD.java*
```java
public abstract class CD implements Packing {
    public abstract String pack();
}
```
*File: Company.java*
```java
public abstract class Company extends CD {
    public abstract int price();
} 
```
##### 3) Create 2 implementation classes of Company: Sony and Samsung
*File: Sony.java*
```java
public class Sony extends Company {
    @Override
    public int price() {
        return 20;
    }

    @Override
    public String pack() {
        return "Sony CD";
    }
}//End of the Sony class.  
```
*File: Samsung.java*
```java
public class Samsung extends Company {
    @Override
    public int price() {
        return 15;
    }

    @Override
    public String pack() {
        return "Samsung CD";
    }
}//End of the Samsung class.  
```
##### 4) Create the CDType class
*File: CDType.java*
```java
import java.util.ArrayList;
import java.util.List;

public class CDType {
    private List<Packing> items = new ArrayList<Packing>();

    public void addItem(Packing packs) {
        items.add(packs);
    }

    public void getCost() {
        for (Packing packs : items) {
            packs.price();
        }
    }

    public void showItems() {
        for (Packing packing : items) {
            System.out.print("CD name : " + packing.pack());
            System.out.println(", Price : " + packing.price());
        }
    }
}//End of the CDType class.  
```
##### 5) Create the CDBuilder class
*File: CDBuilder.java*
```java
public class CDBuilder {
    public CDType buildSonyCD() {
        CDType cds = new CDType();
        cds.addItem(new Sony());
        return cds;
    }

    public CDType buildSamsungCD() {
        CDType cds = new CDType();
        cds.addItem(new Samsung());
        return cds;
    }
}// End of the CDBuilder class.  
```
##### 6) Create the BuilderDemo class
*File: BuilderDemo.java*
```java
public class BuilderDemo {
    public static void main(String args[]) {
        CDBuilder cdBuilder = new CDBuilder();
        CDType cdType1 = cdBuilder.buildSonyCD();
        cdType1.showItems();

        CDType cdType2 = cdBuilder.buildSamsungCD();
        cdType2.showItems();
    }
}  
```
#### [download this builder pattern example](src/builder1.zip)

#### Output of the above example
```java
CD name : Sony CD, Price : 20  
CD name : Samsung CD, Price : 15
```

#### Another Real world example of Builder Pattern
##### UML for Builder Pattern:
We are considering a business case of `pizza-hut` where we can get different varieties of pizza and cold-drink.

`Pizza` can be either a Veg pizza or Non-Veg pizza of several types (like cheese pizza, onion pizza, masala-pizza etc) and will be of 4 sizes i.e. small, medium, large, extra-large.

`Cold-drink` can be of several types (like Pepsi, Coke, Dew, Sprite, Fanta, Maaza, Limca, Thums-up etc.) and will be of 3 sizes small, medium, large.
![Pizza Builder](images/builderuml2.jpg)

##### Real world example of builder pattern
Let's see the step by step real world example of Builder Design Pattern.
- Step 1:**Create an interface Item that represents the Pizza and Cold-drink**.
*File: Item.java*
```java
public interface Item {
    public String name();

    public String size();

    public float price();
}// End of the interface Item.  
```
- Step 2:**Create an abstract class Pizza that will implement to the interface Item**.
*File: Pizza.java*
```java
public abstract class Pizza implements Item {
    @Override
    public abstract float price();
}
```
- Step 3:**Create an abstract class ColdDrink that will implement to the interface Item**.
*File: ColdDrink.java*
```java
public abstract class ColdDrink implements Item {
    @Override
    public abstract float price();
}
```
- Step 4:**Create an abstract class VegPizza that will extend to the abstract class Pizza**.
*File: VegPizza.java*
```java
public abstract class VegPizza extends Pizza {
    @Override
    public abstract float price();

    @Override
    public abstract String name();

    @Override
    public abstract String size();
}// End of the abstract class VegPizza.  
```
- Step 5:**Create an abstract class NonVegPizza that will extend to the abstract class Pizza**.
*File: NonVegPizza.java*
```java
public abstract class NonVegPizza extends Pizza {
    @Override
    public abstract float price();

    @Override
    public abstract String name();

    @Override
    public abstract String size();
}// End of the abstract class NonVegPizza. 
```
- Step 6:**Now, create concrete sub-classes SmallCheezePizza, MediumCheezePizza, LargeCheezePizza, ExtraLargeCheezePizza that will extend to the abstract class VegPizza**.
*File: SmallCheezePizza.java*
```java
public class SmallCheezePizza extends VegPizza {
    @Override
    public float price() {
        return 170.0f;
    }

    @Override
    public String name() {
        return "Cheeze Pizza";
    }

    @Override
    public String size() {
        return "Small size";
    }
}// End of the SmallCheezePizza class.  
```
*File: MediumCheezePizza.java*
```java
public class MediumCheezePizza extends VegPizza {
    @Override
    public float price() {
        return 220.f;
    }

    @Override
    public String name() {
        return "Cheeze Pizza";
    }

    @Override
    public String size() {
        return "Medium Size";
    }
}// End of the MediumCheezePizza class.  
```

*File: LargeCheezePizza.java*
```java
public class LargeCheezePizza extends VegPizza {
    @Override
    public float price() {
        return 260.0f;
    }

    @Override
    public String name() {
        return "Cheeze Pizza";
    }

    @Override
    public String size() {
        return "Large Size";
    }
}// End of the LargeCheezePizza class.  
```

*File: ExtraLargeCheezePizza.java*
```java
public class ExtraLargeCheezePizza extends VegPizza {
    @Override
    public float price() {
        return 300.f;
    }

    @Override
    public String name() {
        return "Cheeze Pizza";
    }

    @Override
    public String size() {
        return "Extra-Large Size";
    }
}// End of the ExtraLargeCheezePizza class.  
```

- Step 7:**Now, similarly create concrete sub-classes SmallOnionPizza, MediumOnionPizza, LargeOnionPizza, ExtraLargeOnionPizza that will extend to the abstract class VegPizza**.

*File: SmallOnionPizza.java*

```java
public class SmallOnionPizza extends VegPizza {
    @Override
    public float price() {
        return 120.0f;
    }

    @Override
    public String name() {
        return "Onion Pizza";
    }

    @Override
    public String size() {
        return "Small Size";
    }
}// End of the SmallOnionPizza class.  
```

*File: MediumOnionPizza.java*
```java
public class MediumOnionPizza extends VegPizza {
    @Override
    public float price() {
        return 150.0f;
    }

    @Override
    public String name() {
        return "Onion Pizza";
    }

    @Override
    public String size() {
        return "Medium Size";
    }
}// End of the MediumOnionPizza class.  
```
*File: LargeOnionPizza.java*
```java
public class LargeOnionPizza extends VegPizza {
    @Override
    public float price() {
        return 180.0f;
    }

    @Override
    public String name() {
        return "Onion Pizza";
    }

    @Override
    public String size() {
        return "Large size";
    }
}// End of the LargeOnionPizza class.  
```

*File: ExtraLargeOnionPizza.java*
```java
public class ExtraLargeOnionPizza extends VegPizza {
    @Override
    public float price() {
        return 200.0f;
    }

    @Override
    public String name() {
        return "Onion Pizza";
    }

    @Override
    public String size() {
        return "Extra-Large Size";
    }
}// End of the ExtraLargeOnionPizza class  
```

- Step 8:**Now, similarly create concrete sub-classes SmallMasalaPizza, MediumMasalaPizza, LargeMasalaPizza, ExtraLargeMasalaPizza that will extend to the abstract class VegPizza.**

*File: SmallMasalaPizza.java*
```java
public class SmallMasalaPizza extends VegPizza {
    @Override
    public float price() {
        return 100.0f;
    }

    @Override
    public String name() {
        return "Masala Pizza";
    }

    @Override
    public String size() {
        return "Samll Size";
    }
}// End of the SmallMasalaPizza class  
```
*File: MediumMasalaPizza.java*
```java
public class MediumMasalaPizza extends VegPizza {

    @Override
    public float price() {
        return 120.0f;
    }

    @Override
    public String name() {

        return "Masala Pizza";

    }

    @Override
    public String size() {
        return "Medium Size";
    }
}
```
*File: LargeMasalaPizza.java*
```java
public class LargeMasalaPizza extends VegPizza {
    @Override
    public float price() {
        return 150.0f;
    }

    @Override
    public String name() {

        return "Masala Pizza";

    }

    @Override
    public String size() {
        return "Large Size";
    }
} //End of the LargeMasalaPizza class  
```

*File: ExtraLargeMasalaPizza.java*
```java
public class ExtraLargeMasalaPizza extends VegPizza {
    @Override
    public float price() {
        return 180.0f;
    }

    @Override
    public String name() {

        return "Masala Pizza";

    }

    @Override
    public String size() {
        return "Extra-Large Size";
    }
}// End of the ExtraLargeMasalaPizza class  
```

- Step 9:**Now, create concrete sub-classes SmallNonVegPizza, MediumNonVegPizza, LargeNonVegPizza, ExtraLargeNonVegPizza that will extend to the abstract class NonVegPizza**.

*File: SmallNonVegPizza.java*
```java
public class SmallNonVegPizza extends NonVegPizza {

    @Override
    public float price() {
        return 180.0f;
    }

    @Override
    public String name() {
        return "Non-Veg Pizza";
    }

    @Override
    public String size() {
        return "Samll Size";
    }

}// End of the SmallNonVegPizza class 
```

*File: MediumNonVegPizza.java*
```java
public class MediumNonVegPizza extends NonVegPizza {

    @Override
    public float price() {
        return 200.0f;
    }

    @Override
    public String name() {
        return "Non-Veg Pizza";
    }

    @Override
    public String size() {
        return "Medium Size";
    }
}
```
*File: LargeNonVegPizza.java*
```java
public class LargeNonVegPizza extends NonVegPizza {

    @Override
    public float price() {
        return 220.0f;
    }

    @Override
    public String name() {
        return "Non-Veg Pizza";
    }

    @Override
    public String size() {
        return "Large Size";
    }

}// End of the LargeNonVegPizza class  
```

*File: ExtraLargeNonVegPizza.java*
```
public class ExtraLargeNonVegPizza extends NonVegPizza {
    @Override
    public float price() {
        return 250.0f;
    }

    @Override
    public String name() {
        return "Non-Veg Pizza";
    }

    @Override
    public String size() {
        return "Extra-Large Size";
    }

}// End of the ExtraLargeNonVegPizza class  
```
- Step 10:**Now, create two abstract classes Pepsi and Coke that will extend abstract class ColdDrink**.

*File: Pepsi.java*
```java
public abstract class Pepsi extends ColdDrink {

    @Override
    public abstract String name();

    @Override
    public abstract String size();

    @Override
    public abstract float price();

}// End of the Pepsi class 
```

*File: Coke.java*
```java
public abstract class Coke extends ColdDrink {

    @Override
    public abstract String name();

    @Override
    public abstract String size();

    @Override
    public abstract float price();

}// End of the Coke class
```

- Step 11: **Now, create concrete sub-classes SmallPepsi, MediumPepsi, LargePepsi that will extend to the abstract class Pepsi.**

*File: SmallPepsi.java*
```java
public class SmallPepsi extends Pepsi {

    @Override
    public String name() {
        return "300 ml Pepsi";
    }

    @Override
    public float price() {
        return 25.0f;
    }

    @Override
    public String size() {
        return "Small Size";
    }
}// End of the SmallPepsi class
```

*File: MediumPepsi.java*
```java
public class MediumPepsi extends Pepsi {

    @Override
    public String name() {
        return "500 ml Pepsi";
    }

    @Override
    public String size() {
        return "Medium Size";
    }

    @Override
    public float price() {
        return 35.0f;
    }
}// End of the MediumPepsi class
```

*File: LargePepsi.java*
```java
public class LargePepsi extends Pepsi {
    @Override
    public String name() {
        return "750 ml Pepsi";
    }

    @Override
    public String size() {
        return "Large Size";
    }

    @Override
    public float price() {
        return 50.0f;
    }
}// End of the LargePepsi class 
```

- Step 12:**Now, create concrete sub-classes SmallCoke, MediumCoke, LargeCoke that will extend to the abstract class Coke**.


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
