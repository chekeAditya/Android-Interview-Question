<h1 align="center">Everything About Java</h1>
- What is Java?
    - Java is a Programming Language and a platform
    - Java was developed by Sun microsystem(which is now the subsidiary{company controlled by holding company} of oracle) in 1995. James Gosling is known as the father of Java. Before java it's Oak but as oak was already registered company team changed to JAVA.
    
- What is Platform?
    - Any hardware and software environment in which a program runs is known as Platform. Since java has a runtime environment (JRE) and API it is called platform.
- Types of Java Application
    1. Standalone Application :- These application are known as desktop application or windows based application. e. g ⇒ Media controller, antivirus etc
    2. Web Application:- Application which runs on server side and create dynamic pages. e. g ⇒  Servlet, JSP, Struts , Spring etc
    3. Enterprise application:- Application which are distributed in nature. It has advantage like high-level security, load balancing. e. g ⇒ banking application.
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
    - JVM :- It is a specification that provides a runtime environment in which Java bytecode can be executed. It can also run those programs which are written in other languages and compiled to Java bytecode.
        - Task Perform :- Loads Code,  Veifies Code, Executes Code, Provide Runtime Environment
    - JRE :- The Java Runtime Environment is a set of software tools which are used for developing Java applications. It is used to provide the runtime environment. It is the implementation of JVM. It physically exists. It contains a set of libraries + other files that JVM uses at runtime.
    - JDK :- The Java Development Kit (JDK) is a software development environment which is used to develop Java applications and applets. It physically exists. It contains JRE + development tools.
        - JDK is the implementation of any one of the below java platform released
            - Standard Edition Java platform
            - Enterprice Edition Java Platform
            - Micro Edition Java Platform
- Collections
    - The **Collection in Java** is a framework that provides an architecture to store and manipulate the group of objects.
    - Java Collections can achieve all the operations that you perform on a data such as searching, sorting, insertion, manipulation, and deletion.
    - Java Collection means a single unit of objects. Java Collection framework provides many interfaces (Set, List, Queue, Deque) and classes ([ArrayList](https://www.javatpoint.com/java-arraylist), Vector, [LinkedList](https://www.javatpoint.com/java-linkedlist), [PriorityQueue](https://www.javatpoint.com/java-priorityqueue), HashSet, LinkedHashSet, TreeSet).
- What is variable in java and variable Hiding (invisible Variable)?
    - Java allows us to declare a variable whenever we need it. We can categorize all our variables into three categories, which have different-different scopes:
        1. **Instance variables**: defined inside a class and have object-level scope.
        2. **Class variables**: defined inside a class with the static keyword. They have class-level scope common to all objects of the same class.
        3. **Local variables**: defined inside a method or in any conditional block. They have block-level scope and are only accessible in the block where they are defined.
        
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
    - Primitive Datatype :- The primitive data types include boolean, char, byte, short, int, long, float and double.
    - Non-Primitive Datatypes :- The non-primitive data types include Classes, Interfaces, and Arrays.
    
    ![https://static.javatpoint.com/images/java-data-types.png](https://static.javatpoint.com/images/java-data-types.png)
