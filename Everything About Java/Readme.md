<h1 align="center">Everything About Java</h1>
- What is Java?
    - Java is a Programming Language and a platform
    - Java was developed by Sun microsystem(which is now the subsidiary{company controlled by holding company} of oracle) in 1995. James Gosling is known as the father of Java. Before java it's Oak but as oak was already registered company team changed to JAVA.
    
- What is Platform?
    - Any hardware and software environment in which a program runs is known as a Platform. Since java has a runtime environment (JRE) and API it is called a platform.
- Types of Java Application
    1. Standalone Application:- These applications are known as desktop applications or windows based applications. e. g ⇒ Media controller, antivirus, etc
    2. Web Application:- Application that runs on the server-side and creates dynamic pages. e. g ⇒  Servlet, JSP, Struts , Spring etc
    3. Enterprise application:- Applications that are distributed in nature. It has advantages like high-level security, load balancing. e. g ⇒ banking applications.
    4. Mobile Application
- Types of Platform (SEMF  → E)
    - 1. Java SE( Java Standard Edition ) ⇒
        - It includes Java programming APIs such as java.lang, [java.io](http://java.io/), [java.net](http://java.net/), java.util, java.sql, java.math etc. It includes core topics like OOPs, String, Regex, Exception, Inner classes, Multithreading, I/O Stream, Networking, AWT, Swing, Reflection, Collection, etc.
    1. Java EE ( Java Enterprise Edition) ⇒ It is an enterprise platform that is mainly used to develop web and enterprise applications. It is built on top of the Java SE platform. It includes topics like Servlet, JSP, Web Services, EJB, JPA, etc
    2. Java ME( Java Micro Edtion) ⇒ It is micro platform that is dedicated to mobile applications.
    3. Java Fx ⇒ It is used to develop rich internet applications. It uses a lightweight user interface API.
- History of Java
    - GreenTalk → Oak → Java ( Name's of Java ) and it's earlier extension was .gt
    - Java is an island in Indonesia where the first coffee was produced (called Java coffee)
    - Java Version History
        
        Many java versions have been released till now. The current stable release of Java is Java SE 10.
        
        1. JDK Alpha and Beta (1995)
        2. JDK 1.0 (23rd Jan 1996)
        3. JDK 1.1 (19th Feb 1997)
        4. J2SE 1.2 (8th Dec 1998)
        5. J2SE 1.3 (8th May 2000)
        6. J2SE 1.4 (6th Feb 2002)
        7. J2SE 5.0 (30th Sep 2004)
        8. Java SE 6 (11th Dec 2006)
        9. Java SE 7 (28th July 2011)
        10. Java SE 8 (18th Mar 2014)
        11. Java SE 9 (21st Sep 2017)
        12. Java SE 10 (20th Mar 2018)
        13. Java SE 11 (September 2018)
        14. Java SE 12 (March 2019)
        15. Java SE 13 (September 2019)
        16. Java SE 14 (Mar 2020)
        17. Java SE 15 (September 2020)
        18. Java SE 16 (Mar 2021)
        19. Java SE 17 (September 2021)
        20. Java SE 18 (to be released by March 2022)
        
        Since Java SE 8 release, the Oracle corporation follows a pattern in which every even version is release in March month and an odd version released in September month.
        
    
    # 
    
- Features of Java
    1. [Simple](https://www.javatpoint.com/features-of-java#Simple)
    - 2.[Object-Oriented](https://www.javatpoint.com/features-of-java#Object-Oriented)
        
        Object-oriented means we organize our software as a combination of different types of objects that incorporate both data and behavior.
        
    1. [Portable](https://www.javatpoint.com/features-of-java#Portable)
    2. [Platform independent](https://www.javatpoint.com/features-of-java#Platform-independent)
    3. [Secured](https://www.javatpoint.com/features-of-java#Secured)
    4. [Robust](https://www.javatpoint.com/features-of-java#Robust)
    5. [Architecture neutral](https://www.javatpoint.com/features-of-java#Architecture-neutral)
    6. [Interpreted](https://www.javatpoint.com/features-of-java#Interpreted)
    7. [High Performance](https://www.javatpoint.com/features-of-java#High-Performance)
    8. [Multithreaded](https://www.javatpoint.com/features-of-java#Multithreaded)
    9. [Distributed](https://www.javatpoint.com/features-of-java#Distributed)
    10. [Dynamic](https://www.javatpoint.com/features-of-java#Dynamic)
- Difference between JDK, JRE, and JVM
    - JVM:- It is a specification that provides a runtime environment in which Java bytecode can be executed. It can also run those programs which are written in other languages and compiled to Java bytecode.
        - Task Perform:- Loads Code,  Verifies Code, Executes Code, Provide Runtime Environment
    - JRE:- The Java Runtime Environment is a set of software tools that are used for developing Java applications. It is used to provide the runtime environment. It is the implementation of JVM. It physically exists. It contains a set of libraries + other files that JVM uses at runtime.
    - JDK:- The Java Development Kit (JDK) is a software development environment that is used to develop Java applications and applets. It physically exists. It contains JRE + development tools.
        - JDK is the implementation of any one of the below java platforms released
            - Standard Edition Java platform
            - Enterprise Edition Java Platform
            - Micro Edition Java Platform
- Collections
    - The **Collection in Java** is a framework that provides an architecture to store and manipulate a group of objects.
    - Java Collections can achieve all the operations that you perform on data such as searching, sorting, insertion, manipulation, and deletion.
    - Java Collection means a single unit of objects. Java Collection framework provides many interfaces (Set, List, Queue, Deque) and classes ([ArrayList](https://www.javatpoint.com/java-arraylist), Vector, [LinkedList](https://www.javatpoint.com/java-linkedlist), [PriorityQueue](https://www.javatpoint.com/java-priorityqueue), HashSet, LinkedHashSet, TreeSet).
- What is variable in java and variable Hiding (invisible Variable)?
    - Java allows us to declare a variable whenever we need it. We can categorize all our variables into three categories, which have different-different scopes:
        1. **Instance variables**: defined inside a class and have object-level scope.
        2. **Class variables**: defined inside a class with the static keyword. They have class-level scope common to all objects of the same class.
        3. **Local variables**: defined inside a method or in any conditional block. They have the block-level scope and are only accessible in the block where they are defined.
        
        **public** **class** A{
        
        **static** **int** m=100;      //static variable
        
        **void** method(){
        
        **int** n=90;       //local variable
        
        }
        
        **public** **static** **void** main(String args[]){
        
        **int** data=50;             //instance variable
        
        }
        
        }//end of class
        
- Datatypes in Java
    - Primitive Datatype:- The primitive data types include boolean, char, byte, short, int, long, float, and double.
    - Non-Primitive Datatypes:- The non-primitive data types include Classes, Interfaces, and Arrays.
    
    ![https://static.javatpoint.com/images/java-data-types.png](https://static.javatpoint.com/images/java-data-types.png)
    
- Operators in Java
    - Unary Operator,
    - Arithmetic Operator,
    - Shift Operator,
    - Relational Operator,
    - Bitwise Operator,
    - Logical Operator,
    - Ternary Operator and
    - Assignment Operator.
    
    [Java Operator Precedence](https://www.notion.so/b73082171fc549689d212849a7179adc)
    
- Keywords
    
    # List of Java Keywords
    
    A list of Java keywords or reserved words are given below:
    
    1. **[abstract](https://www.javatpoint.com/abstract-keyword-in-java):** Java abstract keyword is used to declare an abstract class. An abstract class can provide the implementation of the interface. It can have abstract and non-abstract methods.
    2. **[boolean:](https://www.javatpoint.com/boolean-keyword-in-java)** Java boolean keyword is used to declare a variable as a boolean type. It can hold True and False values only.
    3. **[break](https://www.javatpoint.com/java-break):** Java break keyword is used to break the loop or switch statement. It breaks the current flow of the program at specified conditions.
    4. **[byte](https://www.javatpoint.com/byte-keyword-in-java):** Java byte keyword is used to declare a variable that can hold 8-bit data values.
    5. **[case](https://www.javatpoint.com/case-keyword-in-java):** Java case keyword is used with the switch statements to mark blocks of text.
    6. **[catch](https://www.javatpoint.com/try-catch-block):** Java catch keyword is used to catch the exceptions generated by try statements. It must be used after the try block only.
    7. **[char](https://www.javatpoint.com/char-keyword-in-java):** Java char keyword is used to declare a variable that can hold unsigned 16-bit Unicode characters
    8. **[class](https://www.javatpoint.com/class-keyword-in-java):** Java class keyword is used to declare a class.
    9. **[continue](https://www.javatpoint.com/java-continue):** Java continue keyword is used to continue the loop. It continues the current flow of the program and skips the remaining code at the specified condition.
    10. **[default](https://www.javatpoint.com/default-keyword-in-java):** Java default keyword is used to specify the default block of code in a switch statement.
    11. **[do](https://www.javatpoint.com/java-do-while-loop):** Java do keyword is used in the control statement to declare a loop. It can iterate a part of the program several times.
    12. **[double](https://www.javatpoint.com/double-keyword-in-java):** Java double keyword is used to declare a variable that can hold 64-bit floating-point number.
    13. **[else](https://www.javatpoint.com/java-if-else):** Java else keyword is used to indicate the alternative branches in an if statement.
    14. **[enum](https://www.javatpoint.com/enum-in-java):** Java enum keyword is used to define a fixed set of constants. Enum constructors are always private or default.
    15. **[extends](https://www.javatpoint.com/inheritance-in-java):** Java extends keyword is used to indicate that a class is derived from another class or interface.
    16. **[final](https://www.javatpoint.com/final-keyword):** Java final keyword is used to indicate that a variable holds a constant value. It is used with a variable. It is used to restrict the user from updating the value of the variable.
    17. **[finally](https://www.javatpoint.com/finally-block-in-exception-handling):** Java finally keyword indicates a block of code in a try-catch structure. This block is always executed whether an exception is handled or not.
    18. **[float](https://www.javatpoint.com/float-keyword-in-java):** Java float keyword is used to declare a variable that can hold a 32-bit floating-point number.
    19. **[for](https://www.javatpoint.com/java-for-loop):** Java for keyword is used to start a for loop. It is used to execute a set of instructions/functions repeatedly when some condition becomes true. If the number of iteration is fixed, it is recommended to use for loop.
    20. **[if](https://www.javatpoint.com/java-if-else):** Java if keyword tests the condition. It executes the if block if the condition is true.
    21. **[implements](https://www.javatpoint.com/interface-in-java):** Java implements keyword is used to implement an interface.
    22. **[import](https://www.javatpoint.com/package):** Java import keyword makes classes and interfaces available and accessible to the current source code.
    23. **[instanceof](https://www.javatpoint.com/downcasting-with-instanceof-operator):** Java instanceof keyword is used to test whether the object is an instance of the specified class or implements an interface.
    24. **[int](https://www.javatpoint.com/int-keyword-in-java):** Java int keyword is used to declare a variable that can hold a 32-bit signed integer.
    25. **[interface](https://www.javatpoint.com/interface-in-java):** Java interface keyword is used to declare an interface. It can have only abstract methods.
    26. **[long](https://www.javatpoint.com/long-keyword-in-java):** Java long keyword is used to declare a variable that can hold a 64-bit integer.
    27. **native:** Java native keyword is used to specify that a method is implemented in native code using JNI (Java Native Interface).
    28. **[new](https://www.javatpoint.com/new-keyword-in-java):** Java new keyword is used to create new objects.
    29. **[null](https://www.javatpoint.com/null-keyword-in-java):** Java null keyword is used to indicate that a reference does not refer to anything. It removes the garbage value.
    30. **[package](https://www.javatpoint.com/package):** Java package keyword is used to declare a Java package that includes the classes.
    31. **[private](https://www.javatpoint.com/private-keyword-in-java):** Java private keyword is an access modifier. It is used to indicate that a method or variable may be accessed only in the class in which it is declared.
    32. **[protected](https://www.javatpoint.com/protected-keyword-in-java):** Java protected keyword is an access modifier. It can be accessible within the package and outside the package but through inheritance only. It can't be applied with the class.
    33. **[public](https://www.javatpoint.com/public-keyword-in-java):** Java public keyword is an access modifier. It is used to indicate that an item is accessible anywhere. It has the widest scope among all other modifiers.
    34. **[return](https://www.javatpoint.com/return-keyword-in-java):** Java return keyword is used to return from a method when its execution is complete.
    35. **[short](https://www.javatpoint.com/short-keyword-in-java):** Java short keyword is used to declare a variable that can hold a 16-bit integer.
    36. **[static](https://www.javatpoint.com/static-keyword-in-java):** Java static keyword is used to indicate that a variable or method is a class method. The static keyword in Java is mainly used for memory management.
    37. **[strictfp](https://www.javatpoint.com/strictfp-keyword):** Java strictfp is used to restrict the floating-point calculations to ensure portability.
    38. **[super](https://www.javatpoint.com/super-keyword):** Java super keyword is a reference variable that is used to refer to parent class objects. It can be used to invoke the immediate parent class method.
    39. **[switch](https://www.javatpoint.com/java-switch):** The Java switch keyword contains a switch statement that executes code based on test value. The switch statement tests the equality of a variable against multiple values.
    40. **[synchronized](https://www.javatpoint.com/synchronization-in-java):** Java synchronized keyword is used to specify the critical sections or methods in multithreaded code.
    41. **[this](https://www.javatpoint.com/this-keyword):** Java this keyword can be used to refer the current object in a method or constructor.
    42. **[throw](https://www.javatpoint.com/throw-keyword):** The Java throw keyword is used to explicitly throw an exception. The throw keyword is mainly used to throw custom exceptions. It is followed by an instance.
    43. **[throws](https://www.javatpoint.com/throws-keyword-and-difference-between-throw-and-throws):** The Java throws keyword is used to declare an exception. Checked exceptions can be propagated with throws.
    44. **[transient](https://www.javatpoint.com/transient-keyword):** Java transient keyword is used in serialization. If you define any data member as transient, it will not be serialized.
    45. **[try](https://www.javatpoint.com/try-catch-block):** Java try keyword is used to start a block of code that will be tested for exceptions. The try block must be followed by either catch or finally block.
    46. **void:** Java void keyword is used to specify that a method does not have a return value.
    47. **[volatile](https://www.javatpoint.com/volatile-keyword-in-java):** Java volatile keyword is used to indicate that a variable may change asynchronously.
    48. **[while](https://www.javatpoint.com/java-while-loop):** Java while keyword is used to start a while loop. This loop iterates a part of the program several times. If the number of iteration is not fixed, it is recommended to use the while loop.
- OOPs Concept
    - *Simula* is considered the first object-oriented programming language. The programming paradigm where everything is represented as an object is known as a truly object-oriented programming language.
    - *Smalltalk* is considered the first truly object-oriented programming language.
    - *Objects* An Object can be defined as an instance of a class. An object contains an address and takes up some space in memory. Objects can communicate without knowing the details of each other's data or code. The only necessary thing is the type of message accepted and the type of response returned by the objects.
    - *Class*   *Collection of objects* is called class. It is a logical entity. A class can also be defined as a blueprint from which you can create an individual object. Class doesn't consume any space.
    - *Inheritance* When one object acquires all the properties and behaviors of a parent object, it is known as inheritance. It provides code reusability. It is used to achieve runtime polymorphism.
    - *Polymorphism* When one object acquires all the properties and behaviors of a parent object, it is known as inheritance. It provides code reusability. It is used to achieve runtime polymorphism.
        
        In Java, we use method overloading and method overriding to achieve polymorphism.
        
    - *Abstraction* *Hiding internal details and showing functionality* is known as abstraction. For example phone call, we don't know the internal processing.
        - In Java, we use abstract class and interface to achieve abstraction.
    - *Encapsulation* *Binding (or wrapping) code and data together into a single unit are known as encapsulation*. For example, a capsule is wrapped with different medicines.
        - A java class is an example of encapsulation. Java bean is the fully encapsulated class because all the data members are private here.
