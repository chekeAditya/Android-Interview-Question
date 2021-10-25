- What is Kotlin?
    - Kotlin is a modern Programming language that makes developer happier.
    - Kotlin is a statically-typed programming language which runs on the JVM. It can be compiled either using Java source code and LLVM compiler(LLVM is a set of compiler and toolchain technologies, which can be used to develop a front end for any programming language and a back end for any instruction set architecture).
- Who is the developer of Kotlin?
    
    Kotlin was developed by JetBrains.
    
- Why you should switch to Kotlin from Java?
    - Kotlin language is quite simple compared to Java. It reduces may redundancies in code as compared to Java. Kotlin can offer some useful features which are not supported by Java.
    1. Kotlin language is easy to learn as its syntax is similar to Java.
    2. Kotlin is a functional language and based on JVM. So, it removes lots of boiler plate
    3. It is an expressive language which makes code readable and understandable.
- Explain the use of extension functions?
    
    Extension functions are beneficial for extending class without the need to inherit from the class.
    
    # **1. How does Kotlin work on Android?**

Just like Java, the Kotlin code is also compiled into the Java bytecode and is executed at runtime by the Java Virtual Machine i.e. JVM. When a Kotlin file named `Main.kt` is compiled then it will eventually turn into a class and then the bytecode of the class will be generated. The name of the bytecode file will be `MainKt.class` and this file will be executed by the JVM.

# **2. Why should we use Kotlin?**

- Kotlin is concise
- Kotlin is null-safe
- Kotlin is interoperable

[Learn about these features from MindOrks video](https://www.youtube.com/watch?v=kRhivT-jKzY&list=PL6nth5sRD25iv8jZrQWD-5dXgu56ae5m8).

# **3. What is the difference between the variable declaration with var and val?**

If you want to declare some mutable(changeable) variable, then you can use `var`. For the immutable variable, use `val` i.e. `val` variables can't be changed once assigned.

# **4. What is the difference between the variable declaration with val and const?**

Both the variables that are declared with `val` and `const` are immutable in nature. But the value of the `const` variable must be known at the compile-time whereas the value of the `val` variable can be assigned at runtime also.

[Learn more about the difference between const and val from MindOrks blog](https://blog.mindorks.com/what-is-the-difference-between-const-and-val).

# **5. How to ensure null safety in Kotlin?**

One of the major advantages of using Kotlin is null safety. In Java, if you access some null variable then you will get a `NullPointerException`. So, the following code in Kotlin will produce a compile-time error:

```
var name: String = "MindOrks"
name =null//error
```

So, to assign null values to a variable, you need to declare the `name` variable as a nullable string and then during the access of this variable, you need to use a safe call operator i.e. `?.`

```
var name: String? = "MindOrks"
print(name?.length)// ok
name =null// ok
```

[Learn more about safe calls(?.) and null check(!!) from MindOrks blog](https://blog.mindorks.com/safecalls-vs-nullchecks-in-kotlin).

# **6. What is the difference between safe calls(?.) and null check(!!)?**

Safe call operator i.e. `?.` is used to check if the value of the variable is null or not. If it is null then null will be returned otherwise it will return the desired value.

```
var name: String? = "MindOrks"
println(name?.length)// 8
name =nullprintln(name?.length)// null
```

If you want to throw NullPointerException when the value of the variable is null, then you can use the null check or `!!` operator.

```
var name: String? = "MindOrks"
println(name?.length)// 8
name =nullprintln(name!!.length)// KotlinNullPointerException
```

[Learn more about safe calls(?.) and null check(!!) from MindOrks blog](https://blog.mindorks.com/safecalls-vs-nullchecks-in-kotlin).

# **7. Do we have a ternary operator in Kotlin just like java?**

No, we don't have a ternary operator in Kotlin but you can use the functionality of ternary operator by using if-else or Elvis operator.

# **8. What is Elvis operator in Kotlin?**

In Kotlin, you can assign null values to a variable by using the null safety property. To check if a value is having null value then you can use if-else or can use the Elvis operator i.e. `?:` For example:

```
var name:String? = "Mindorks"
val nameLength = name?.length ?: -1
println(nameLength)
```

The Elvis operator(`?:`) used above will return the length of name if the value is not null otherwise if the value is null, then it will return `-1`.

# **9. How to convert a Kotlin source file to a Java source file?**

Steps to convert your Kotlin source file to Java source file:

1. Open your Kotlin project in the IntelliJ IDEA / Android Studio.
2. Then navigate to **Tools > Kotlin > Show Kotlin Bytecode.**
3. Now click on the **Decompile** button to get your Java code from the bytecode.

[Learn more about the conversion steps from MindOrks blog](https://blog.mindorks.com/how-to-convert-a-kotlin-source-file-to-a-java-source-file).

# **10. What is the use of @JvmStatic, @JvmOverloads, and @JvmFiled in Kotlin?**

- **@JvmStatic:** This annotation is used to tell the compiler that the method is a static method and can be used in Java code.
- **@JvmOverloads:** To use the default values passed as an argument in Kotlin code from the Java code, we need to use the `@JvmOverloads` annotation.
- **@JvmField:** To access the fields of a Kotlin class from Java code without using any getters and setters, we need to use the `@JvmField` in the Kotlin code.

[Learn more about @JvmStatic, @JvmOverloads, and @JvmField in Kotlin from MindOrks blog](https://blog.mindorks.com/jvmstatic-jvmoverloads-and-jvmfield-in-kotlin).

# **11. What is a data class in Kotlin?**

Data classes are those classes which are made just to store some data. In Kotlin, it is marked as data. The following is an example of the same:

```
data classDeveloper(val name: String, val age: Int)
```

When we mark a class as a *data* class, you don’t have to implement or create the following functions like we do in Java: `hashCode()`, `equals()`, `toString()`, `copy()`. The compiler automatically creates these internally, so it also leads to clean code. Although, there are few other requirements that data classes need to fulfill.

[Learn more about data class from MindOrks blog](https://blog.mindorks.com/learn-kotlin-data-class).

# **12. Can we use primitive types such as int, double, float in Kotlin?**

In Kotlin, we can't use primitive types directly. We can use classes like Int, Double, etc. as an object wrapper for primitives. But the compiled bytecode has these primitive types.

# **13. What is String Interpolation in Kotlin?**

If you want to use some variable or perform some operation inside a string then String Interpolation can be used. You can use the `$` sign to use some variable in the string or can perform some operation in between `{}` sign.

```
var name = "MindOrks"
print("Hello! I am learning from $name")
```

# **14. What do you mean by destructuring in Kotlin?**

**Destructuring** is a convenient way of extracting multiple values from data stored in(possibly nested) objects and Arrays. It can be used in locations that receive data (such as the left-hand side of an assignment). Sometimes it is convenient to d*estructure* an object into a number of variables, for example:

```
val (name, age) = developer
```

Now, we can use name and age independently like below:

```
println(name)
println(age)
```

[Learn more about Kotlin Destructuring from MindOrks blog](https://blog.mindorks.com/learn-kotlin-destructuring-declarations).

# **15. When to use the lateinit keyword in Kotlin?**

`lateinit` is late initialization.

Normally, properties declared as having a non-null type must be initialized in the constructor. However, fairly often this is not convenient.

For example, properties can be initialized through dependency injection, or in the setup method of a unit test. In this case, you cannot supply a non-null initializer in the constructor, but you still want to avoid null checks when referencing the property inside the body of a class. To handle this case, you can mark the property with the lateinit modifier.

[Learn more about lateinit from MindOrks blog](https://blog.mindorks.com/learn-kotlin-lateinit-vs-lazy).

# **16. How to check if a lateinit variable has been initialized or not?**

You can check if the lateinit variable has been initialized or not before using it with the help of `isInitialized` method. This method will return true if the lateinit property has been initialized otherwise it will return false. For example:

```
classPerson {
 lateinit var name: String
 funinitializeName() {
 println(this::name.isInitialized)
 name = "MindOrks"// initializing name
 println(this::name.isInitialized)
 }
}
funmain(args: Array<String>) {
 Person().initializeName()
}
```

[Learn more about it from MindOrks blog](https://blog.mindorks.com/how-to-check-if-a-lateinit-variable-has-been-initialized).

# **17. What is the difference between lateinit and lazy in Kotlin?**

- lazy can only be used for val properties, whereas lateinit can only be applied to var because it can’t be compiled to a final field, thus no immutability can be guaranteed.
- If you want your property to be initialized from outside in a way probably unknown beforehand, use lateinit.

[Learn more about the difference between lateinit and lazy from MindOrks blog](https://blog.mindorks.com/learn-kotlin-lateinit-vs-lazy).

# **18. Is there any difference between == operator and === operator?**

Yes. The `==` operator is used to compare the values stored in variables and the `===` operator is used to check if the reference of the variables are equal or not. But in the case of primitive types, the `===` operator also checks for the value and not reference.

```
// primitive example
val int1 = 10
val int2 = 10
println(int1 == int2)// true
println(int1 === int2)// true// wrapper example
val num1 = Integer(10)
val num2 = Integer(10)
println(num1 == num2)// true
println(num1 === num2)//false
```

# **19. What is the forEach in Kotlin?**

In Kotlin, to use the functionality of a for-each loop just like in Java, we use a `forEach` function. The following is an example of the same:

```
var listOfMindOrks = listOf("mindorks.com", "blog.mindorks.com", "afteracademy.com")
listOfMindOrks.forEach {
 Log.d(TAG,it)
}
```

# **20. What are companion objects in Kotlin?**

In Kotlin, if you want to write a function or any member of the class that can be called without having the instance of the class then you can write the same as a member of a companion object inside the class.

To create a **companion** object, you need to add the `companion` keyword in front of the object declaration.

The following is an example of a companion object in Kotlin:

```
classToBeCalled {
 companion object Test {
 funcallMe() = println("You are calling me :)")
 }
}
funmain(args: Array<String>) {
 ToBeCalled.callMe()
}
```

[Learn more about companion object from MindOrks blog](https://blog.mindorks.com/companion-object-in-kotlin).

# **21. What is the equivalent of Java static methods in Kotlin?**

To achieve the functionality similar to Java static methods in Kotlin, we can use:

- companion object
- package-level function
- object

[Read more about this from MindOrks blog](https://blog.mindorks.com/what-is-the-equivalent-of-java-static-methods-in-kotlin).

# **22. What is the difference between FlatMap and Map in Kotlin?**

- FlatMap is used to combine all the items of lists into one list.
- Map is used to transform a list based on certain conditions.

[Read more about FlatMap and Map in Kotlin from MindOrks blog](https://blog.mindorks.com/flatmap-vs-map-in-kotlin).

# **23. What is the difference between List and Array types in Kotlin?**

If you have a list of data that is having a fixed size, then you can use an Array. But if the size of the list can vary, then we have to use a mutable list.

[Learn more about the difference between List and Array from MindOrks blog](https://blog.mindorks.com/difference-between-list-and-array-types-in-kotlin).

# **24. Can we use the new keyword to instantiate a class object in Kotlin?**

No, in Kotlin we don't have to use the `new` keyword to instantiate a class object. To instantiate a class object, simply we use:

```
var varName = ClassName()
```

# **25. What are visibility modifiers in Kotlin?**

A visibility modifier or access specifier or access modifier is a concept that is used to define the scope of something in a programming language. In Kotlin, we have four visibility modifiers:

- **private:** visible inside that particular class or file containing the declaration.
- **protected:** visible inside that particular class or file and also in the subclass of that particular class where it is declared.
- **internal:** visible everywhere in that particular module.
- **public:** visible to everyone.

Note: By default, the visibility modifier in Kotlin is **public**.

[Learn more about visibility modifiers in Kotlin from MindOrks blog](https://blog.mindorks.com/learn-kotlin-visibility-modifiers-private-protected-internal-public).

# **26. How to create a Singleton class in Kotlin?**

A singleton class is a class that is defined in such a way that only one instance of the class can be created and is used where we need only one instance of the class like in logging, database connections, etc.

To create a Singleton class in Kotlin, you need to use the object keyword.

```
object AnySingletonClassName
```

> Note: You can't use constructor in object, but you can use init.
> 

[Learn more about Singleton class from MindOrks blog](https://blog.mindorks.com/how-to-create-a-singleton-class-in-kotlin).

# **27. What are init blocks in Kotlin?**

`init` blocks are initializer blocks that are executed just after the execution of the primary constructor. A class file can have one or more init blocks that will be executed in series. If you want to perform some operation in the primary constructor, then it is not possible in Kotlin, for that, you need to use the `init` block.

[Learn more about init blocks from MindOrks blog](https://blog.mindorks.com/understanding-init-block-in-kotlin).

# **28. What are the types of constructors in Kotlin?**

- **Primary constructor:** These constructors are defined in the class header and you can't perform some operation in it, unlike Java's constructor.
- **Secondary constructor:** These constructors are declared inside the class body by using the constructor keyword. You must call the primary constructor from the secondary constructor explicitly. Also, the property of the class can’t be declared inside the secondary constructor. There can be more than one secondary constructors in Kotlin.

[Learn more about Primary and Secondary constructors from MindOrks blog](https://blog.mindorks.com/primary-and-secondary-constructors-in-kotlin).

# **29. Is there any relationship between primary and secondary constructors?**

Yes, when using a secondary constructor, you need to call the primary constructor explicitly.

# **30. What is the default type of argument used in a constructor?**

By default, the type of arguments of a constructor in val. But you can change it to var explicitly.

# **31. What are Coroutines in Kotlin?**

A framework to manage concurrency in a more performant and simple way with its lightweight thread which is written on top of the actual threading framework to get the most out of it by taking the advantage of cooperative nature of functions.

**This is an important interview question**.

[Learn more about Kotlin Coroutines with examples from MindOrks blog](https://blog.mindorks.com/mastering-kotlin-coroutines-in-android-step-by-step-guide).

# **32. What is suspend function in Kotlin Coroutines?**

Suspend function is the building block of the Coroutines in Kotlin. Suspend function is a function that could be started, paused, and resume. To use a suspend function, we need to use the suspend keyword in our normal function definition.

[Learn more about the suspend function from MindOrks blog](https://blog.mindorks.com/suspend-function-in-kotlin-coroutines).

# **33. What is the difference between Launch and Async in Kotlin Coroutines?**

The difference is that the `launch{}` does not return anything and the `async{}` returns an instance of `Deferred<T>`, which has an `await()` function that returns the result of the coroutine like we have future in Java in which we do `future.get()` to the get the result.

In other words:

- launch: fire and forget
- async: perform a task and return a result

[Learn more about Launch vs Async from MindOrks video](https://www.youtube.com/watch?v=nC30UiDv8Xc).

# **34. What are scopes in Kotlin Coroutines?**

[Learn from MindOrks blog](https://blog.mindorks.com/mastering-kotlin-coroutines-in-android-step-by-step-guide).

# **35. How Exception Handling is done in Kotlin Coroutines?**

[Learn from MindOrks blog](https://blog.mindorks.com/exception-handling-in-kotlin-coroutines).

# **36. How to choose between a switch and when in Kotlin?**

Whenever we want to handle many if-else conditions, then we generally use switch-case statements. But Kotlin provides a more concise option i.e. in Kotlin, we can use when in place of the switch. And, when can be used as:

- expression
- arbitrary condition expression
- without argument
- with two or more choices

For example:

```
when(number) {
 1 -> println("One")
 2, 3 -> println("Two or Three")
 4 -> println("Four")
else -> println("Number is not between 1 and 4")
}
```

[Learn more about when from MindOrks blog](https://blog.mindorks.com/replace-switch-with-when-in-kotlin).

# **37. What is the open keyword in Kotlin used for?**

By default, the classes and functions are final in Kotlin. So, you can't inherit the class or override the functions. To do so, you need to use the open keyword before the class and function. For example:

[Learn more about open keyword from MindOrks blog](https://blog.mindorks.com/understanding-open-keyword-in-kotlin).

# **38. What are lambdas expressions?**

Lambdas expressions are anonymous functions that can be treated as values i.e. we can pass the lambdas expressions as arguments to a function return them, or do any other thing we could do with a normal object. For example:

```
val add : (Int, Int) -> Int = { a, b -> a + b }
val result = add(9, 10)
```

[Learn more about Lambdas from MindOrks blog](https://blog.mindorks.com/understanding-higher-order-functions-and-lambdas-in-kotlin).

# **39. What are Higher-Order functions in Kotlin?**

A higher-order function is a function that takes functions as parameters or returns a function. For example, A function can take functions as parameters.

```
funpassMeFunction(abc: () -> Unit) {
// I can take function// do something here// execute the function
 abc()
}
```

For example, A function can return another function.

```
funadd(a: Int, b: Int): Int {
return a + b
}
```

And, we have a function **returnMeAddFunction** which takes zero parameters and returns a function of the type **((Int, Int) -> Int)**.

```
funreturnMeAddFunction(): ((Int, Int) -> Int) {
// can do something and return function as well// returning functionreturn ::add
}
```

And to call the above function, we can do:

```
val add = returnMeAddFunction()
val result = add(2, 2)
```

[Learn more about Higher-Order functions from MindOrks blog](https://blog.mindorks.com/understanding-higher-order-functions-and-lambdas-in-kotlin).

# **40. What are extension functions in Kotlin?**

Extension functions are like extensive properties attached to any class in Kotlin. By using extension functions, you can add some methods or functionalities to an existing class even without inheriting the class. For example: Let's say, we have views where we need to play with the visibility of the views. So, we can create an extension function for views like,

```
fun View.show() {
this.visibility = View.VISIBLE
}

fun View.hide() {
this.visibility = View.GONE
}
```

and to use it we use, like,

```
toolbar.hide()
```

[Learn more about extension functions from MindOrks blog](https://blog.mindorks.com/extension-functions-vs-static-utility-class).

# **41. What is an infix function in Kotlin?**

An infix function is used to call the function without using any bracket or parenthesis. You need to use the infix keyword to use the infix function.

```
classOperations {
 var x = 10;
 infix funminus(num: Int) {
this.x =this.x - num
 }
}
funmain() {
 val opr = Operations()
 opr minus 8
 print(opr.x)
}
```

# **42. What is an inline function in Kotlin?**

Inline function instruct compiler to insert complete body of the function wherever that function got used in the code. To use an Inline function, all you need to do is just add an inline keyword at the beginning of the function declaration.

[Learn more about Inline functions from MindOrks blog](https://blog.mindorks.com/understanding-inline-noinline-and-crossinline-in-kotlin).

# **43. What is noinline in Kotlin?**

While using an inline function and want to pass some lambda function and not all lambda function as inline, then you can explicitly tell the compiler which lambda it shouldn't inline.

```
inline fundoSomethingElse(abc: () -> Unit, noinline xyz: () -> Unit) {
 abc()
 xyz()
}
```

[Learn more about noinline functions from MindOrks blog](https://blog.mindorks.com/understanding-inline-noinline-and-crossinline-in-kotlin).

# **44. What are Reified types in Kotlin?**

When you are using the concept of Generics to pass some class as a parameter to some function and you need to access the type of that class, then you need to use the reified keyword in Kotlin.

For example:

```
inline fun <reified T> genericsExample(value: T) {
 println(value)
 println("Type of T: ${T::class.java}")
}
funmain() {
 genericsExample<String>("Learning Generics!")
 genericsExample<Int>(100)
}
```

[Learn more about Reified keyword from MindOrks blog](https://blog.mindorks.com/what-are-reified-types-in-kotlin).

# **45. What is the operator overloading in Kotlin?**

In Kotlin, we can use the same operator to perform various tasks and this is known as operator overloading. To do so, we need to provide a member function or an extension function with a fixed name and operator keyword before the function name because normally also, when we are using some operator then under the hood some function gets called. For example, if you are writing `num1+num2`, then it gets converted to `num1.plus(num2)`.

For example:

```
funmain() {
 val bluePen = Pen(inkColor = "Blue")
 bluePen.showInkColor()

 val blackPen = Pen(inkColor = "Black")
 blackPen.showInkColor()

 val blueBlackPen = bluePen + blackPen
 blueBlackPen.showInkColor()
}

 operator fun Pen.plus(otherPen: Pen):Pen{
 val ink = "$inkColor, ${otherPen.inkColor}"return Pen(inkColor = ink)
 }

 data classPen(val inkColor:String){
 funshowInkColor(){ println(inkColor)}
 }
```

[Learn more about operator overloading from MindOrks blog](https://blog.mindorks.com/operator-overloading-in-kotlin).

# **46. Explain the use-case of let, run, with, also, apply in Kotlin.**

[Learn from MindOrks blog](https://blog.mindorks.com/using-scoped-functions-in-kotlin-let-run-with-also-apply).

# **47. What are pair and triple in Kotlin?**

Pair and Triples are used to return two and three values respectively from a function and the returned values can be of the same data type or different.

```
val pair = Pair("My Age: ", 25)
print(pair.first + pair.second)
```

[Learn more about Pairs and Triples from MindOrks blog](https://blog.mindorks.com/pair-and-triple-in-kotlin).

# **48. What are labels in Kotlin?**

Any expression written in Kotlin is called a label. For example, if we are having a *for-loop* in our Kotlin code then we can name that *for-loop* expression as a label and will use the label name for the *for-loop*.

We can create a label by using an identifier followed by the `@` sign. For example, `name@`, `loop@`, `xyz@`, etc. The following is an example of a label:

```
loop@for (i in 1..10) {
// some code goes here
}
```

The name of the above for-loop is `loop`.

[Learn more about labels in Kotlin from MindOrks blog](https://blog.mindorks.com/learn-kotlin-returns-jumps-labels).

# **49. What are the benefits of using a Sealed Class over Enum?**

Sealed classes give us the flexibility of having **different** **types of subclasses and also containing the state**. The important point to be noted here is the subclasses that are extending the Sealed classes should be either nested classes of the Sealed class or should be declared in the same file as that of the Sealed class.

[Learn more about Sealed classes from MindOrks blog](https://blog.mindorks.com/learn-kotlin-sealed-classes).

# **50. What are collections in Kotlin?**

[Learn from MindOrks video](https://www.youtube.com/watch?v=XeRt2ZZ-jkA).

Prepare these 50 questions for your interview and also go through the given link in each question to have a better knowledge of the topic.
    
- What does ‘Null Safety’ mean in Kotlin?
    
    Null Safety feature allows removing the risk of occurrence of NullPointerException in real time. It is also possible to differentiate between nullable references and non-nullable references.
    
- How does Kotlin work on Android
- How Retrofit works Externally?
    
    What :- Retrofit is a type-safe HTTP client for Android and Java.
    
    Why:- Using Retrofit made networking easier in Android apps. As it has many features like easy to add custom headers and request types, file uploads, mocking responses, etc through which we can reduce boilerplate code in our apps and consume the web service easily.
    
    How:-    A model class which is used as a **JSON** model
    
    - An interface that defines the **HTTP** operations needs to be performed
    - Retrofit.Builder class: Instance which uses the interface defined above and the Builder API to allow defining the **URL endpoint** for the **HTTP** operations. It also takes the **converters** we provide to format the **Response**.
- Explain Permission and their types?
    
    **Important Points in Permission:**
    
    - Runtime permission come in picture after marshmallow version before that only in manifest the permission need to declare. But from marshmallow version we need to declare in manifest as well as we have to request permission at runtime.
    - From the Lollypop version android categorized the permissions into two categories that are **Normal Permission**: Which are declared in manifest and auto granted by android without asking user.    eg, Internet Permission, Network state access, etc.                                                  **Dangerous Permission**: Android doesn't grant permissions by default, they need to ask user permission to be granted to access the services or data. eg, Location Permission, Reading or Writing data
    
    App permissions help support user privacy by protecting access to the following:
    
    - **Restricted data**, such as system state and a user's contact information.
    - **Restricted actions**, such as connecting to a paired device and recording audio.
    
    ![https://developer.android.com/images/training/permissions/workflow-overview.svg](https://developer.android.com/images/training/permissions/workflow-overview.svg)
    
    Types of Permissions→
    
    - Install-time permission: ⇒
        1. this permission give your app limited access to restricted data and all app to perform restricted action that minimally affect the s/y or other apps.
        2. at install-time permission s/y automatically grants permission in your app.
    - Normal Permission ⇒
        
        this permission allow access to the data and actions that extends beyond your's sandbox. Data and actions persent very little risk to the user's privacy and operation of the other apps.
        
    - Signature Permission ⇒
        1. If the app declares a signature permission that another app has defined, and if the two apps are signed by the same certificate, then the system grants the permission to the first app at install time. Otherwise, that first app cannot be granted the permission.
        2. if you write App A that defends itself with a signature-level permission (e.g., a custom one), and you write App B that wants to talk to the defended portions of App A, you can do so, if you are signing App A and App B with the same signing key.
    - Runtime Permissions
        1. This give your app additional access to restricted data, and they allow your app to perform restricted actions that more substantially affect the system and other apps.
        2. Therefore, you need to request runtime permissions in your app before you can access the restricted data or perform restricted actions
        3. Many runtime permissions access private user data, a special type of restricted data that includes potentially sensitive information. Examples of private user data include location and contact information.
    - Special Permissions ⇒
        
        Special permissions correspond to particular app operations. Only the platform and OEMs can define special permissions. Additionally, the platform and OEMs usually define special permissions when they want to protect access to particularly powerful actions, such as drawing over other apps.
        
    
- What is MVVM Architecture?
    
    *MVM architecture is a Model-View-ViewModel architecture that removes the tight coupling between each component. Most importantly, in this architecture, the children don't have the direct reference to the parent, they only have the reference by observables.
    
    ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/mvvm.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/mvvm.png)
    
    - **Model:** It represents the data and the business logic of the Android Application. It consists of the business logic - local and remote data source, model classes, repository.
    - **View:** It consists of the UI Code(Activity, Fragment), XML. It sends the user action to the ViewModel but does **not** get the response back directly. To get the response, it has to subscribe to the observables which ViewModel exposes to it.
    - **ViewModel:** It is a bridge between the View and Model(business logic). It does not have any clue which View has to use it as it does not have a direct reference to the View. So basically, the ViewModel should not be aware of the view who is interacting with. It interacts with the Model and exposes the observable that can be observed by the View.
- Explain ViewModel?
    - The ViewModel class is designed to store and manage UI-related data in a lifecycle conscious way. The ViewModel class allows data to survive configuration changes such as screen rotations.
    - The view model behaves as a bridge between view and the model.
    - When the owner activity is finished, the framework calls the ViewModel objects's onCleared() method so that it can clean up resources.
    - The ViewModel exists from when the you first request a ViewModel (usually in the onCreate the Activity) until the Activity is finished and destroyed. onCreate may be called several times during the life of an Activity, such as when the app is rotated, but the ViewModel survives throughout.
    
    Lifecycler of a ViewModel
    
    ![https://developer.android.com/images/topic/libraries/architecture/viewmodel-lifecycle.png](https://developer.android.com/images/topic/libraries/architecture/viewmodel-lifecycle.png)
    
    The ViewModel exists from when you first request a ViewModel until the activity is finished and destroyed.
    
    ---
    
    ViewModel Implementattion without live data
    
    Step:1 Create a ViewModel class
    
    ```kotlin
    public class ScoreViewModel extends ViewModel {
       // Tracks the score for Team A
       public int scoreTeamA = 0;
    
       // Tracks the score for Team B
       public int scoreTeamB = 0;
    }
    ```
    
    Step:2 Associate the UI Controller and ViewModel
    
    ```kotlin
    ViewModelProviders.of(<Your UI controller>).get(<Your ViewModel>.class)
    //In the case of Court-Counter, this looks like:
    @Override
    protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       mViewModel = ViewModelProviders.of(this).get(ScoreViewModel.class);
       // Other setup code below...
    }
    ```
    
    Step:3 Use the ViewModel in your UI Controller
    
    ```kotlin
    // The finished onCreate method
    @Override
    protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       mViewModel = ViewModelProviders.of(this).get(ScoreViewModel.class);
       displayForTeamA(mViewModel.scoreTeamA);
       displayForTeamB(mViewModel.scoreTeamB);
    }
    
    // An example of both reading and writing to the ViewModel
    public void addOneForTeamA(View v) {
       mViewModel.scoreTeamA = mViewModel.scoreTeamA + 1;
       displayForTeamA(mViewModel.scoreTeamA);
    }
    ```
    
- Explaing ViewModelsProvidets.of ?
    - The first time the ViewModelProviders.of method is called by MainActivity, it creates a new ViewModel instance. When this method is called again, which happens whenever onCreate is called, it will return the pre-existing ViewModel associated with the specific Court-Counter MainActivity. This is what preserves the data.
    
    ```kotlin
    ViewModelProviders.of(<THIS ARGUMENT>).get(ScoreViewModel.class);
    ```
    
- Conclusion on ViewModels
    - The [ViewModel](https://developer.android.com/reference/android/arch/lifecycle/ViewModel.html) class is designed to hold and manage UI-related data in a life-cycle conscious way. This allows data to survive configuration changes such as screen rotations.
    - ViewModels separate UI implementation from your app’s data.
    - In general, if a screen in your app has transient data, you should create a separate ViewModel for that screen’s data.
    - The lifecycle of a ViewModel extends from when the associated UI controller is first created, till it is completely destroyed.
    - Never store a UI controller or Context directly or indirectly in a ViewModel. This includes storing a View in a ViewModel. Direct or indirect references to UI controllers defeat the purpose of separating the UI from the data and can lead to memory leaks.
    - ViewModel objects will often store LiveData objects, which you can learn more about [here](https://developer.android.com/topic/libraries/architecture/livedata.html).
    - The [ViewModelProviders.of](https://developer.android.com/reference/android/arch/lifecycle/ViewModelProviders.html#of(android.support.v4.app.Fragment)) method keeps track of what UI controller the ViewModel is associated with via the UI controller that is passed in as an argument.
- Live Data
    - LiveData is an observable data holder class. Unlike a regular observable, LiveData is lifecycle-aware, meaning it respects the lifecycle of other app components, such as activities, fragments, or services. This awareness ensures LiveData only updates app component observers that are in an active lifecycle state.
    - Advantage of liveData:-
        - No memory leaks
        - Views always get the up to date data
        - No crash due to stopped activities
    - In Simple Words
        
        LiveData is basically a data holder and it is used to observe the changes of a particular view and then update the corresponding change. It is lifecycle-aware i.e. whenever a data is updated or changed then the updates will be sent to only those app components which are in active state. If the app component is not active and in the future, if it becomes active, then the updated data will be sent to that app component. So, you need not worry about the lifecycle of the app component while updating data.
        
        ---
        
        For example, if you are not using LiveData and you are updating some TextView with some value, then on rotation of the screen, you need to again set the new value in the TextView because the Activity will be recreated on screen rotation. But if you are using LiveData, all you need to do is just update the value and that's it. No need to care about the lifecycle.
        
    - Steps to work with live data
        1. Firstly, for holding the data, you need to create a LiveData instance in your ViewModel.
        2. After creating the instance of LiveData, you need to set the data in the LiveData by using methods like `setValue` and `postValue`.
        3. After that, you need to return the LiveData so that it can be observed by some observer in the views like Activity or Fragments.
        4. And finally, you need to observe the data in your views with the help of `observe` method. In the observer, you need to define all the changes in the UI that you want to perform on data change.
- SetValue and PostValue in LiveData?
    
    When we need to change/update the data in LiveData. The MutableLiveData publicly exposes two methods i.e. setValue and postValue to set the data in LiveData.
    
    So, here are some of the points that you must think before using `setValue` and `postValue`:
    
    - If you are working on the main thread, then both `setValue` and `postValue` will work in the same manner i.e. they will update the value and notify the observers.
    - If working in some background thread, then you can't use `setValue`. You have to use `postValue` here with some observer. But the interesting thing about `postValue` is that the value will be change immediately but the notification that is to be sent to observers will be scheduled to execute on the main thread via the event loop with the handler.
    - Example
        
        ```kotlin
        // setValue
        liveData.setValue("someNewData")
        liveData.setValue("againNewData")
        
        // postValue
        liveData.postValue("someNewData")
        liveData.postValue("againNewData")
        ```
        
        In the above example, the `setValue` is called from the main thread and the `postValue` is called from some background thread.
        
        Since the `setValue` is called twice, so the value will be updated twice and the observers will receive the notification regarding the updated data twice.
        
        But for `postValue`, the value will be updated twice and **the number of times the observers will receive the notification depends on the execution of the main thread.** For example, if the `postValue` is called 4 times before the execution of the main thread, then the observer will receive the notification only once and that too with the latest updated data because the notification to be sent is scheduled to be executed on the main thread. So, if you are calling the `postValue` method a number of times before the execution of the main thread, then the value that is passed lastly i.e. the latest value will be dispatched to the main thread and rest of the values will be discarded.
        
        Another thing to care about `postValue` is that, if the field on which the `postValue` is called is not having any observers and after that, you call the `getValue`, then you will not receive the value that you set in the `postValue` because you don't have an observer here.
        
- What is Coroutine?
    
    Coroutines = Co + Routines
    
    - Here, Co means cooperation and Routines means functions.
    - When function cooperates with each other, we call it as Coroutines.
    - Coroutines, a very efficient and complete framework to manage concurrency(2 or more things working parallelly in a more performant and simple way.
    - The Difference between threads and coroutine are Threads are managed by OS and Coroutine are managed by Users.
    - Coroutines are lightweight threads. A lightweight thread means it doesn’t map on the native thread, so it doesn’t require context switching on the processor, so they are faster.
    - Example:-
        
        Here, **functionA** will do the **taskA1** and give control to the **functionB** to execute the **taskB1**.
        
        Then, **functionB** will do the **taskB1** and give the control back to the **functionA** to execute the **taskA2** and so on.
        
        The important thing is that functionA and functionB are cooperating with each other.
        
        With Kotlin Coroutines, the above cooperation can be done very easily which is without the use of **when** or **switch** **case** which I have used in the above example for the sake of understanding.
        
        Now that, we have understood what are coroutines when it comes to cooperation between the functions. There are endless possibilities that open up because of the cooperative nature of functions.
        
        A few of the possibilities are as follows:
        
        - It can execute a few lines of functionA and then execute a few lines of functionB and then again a few lines of functionA and so on. **This will be helpful when a thread is sitting idle not doing anything, in that case, it can execute a few lines of another function. This way, it can take the full advantage of thread.** Ultimately the cooperation helps in multitasking.
        - It will enable writing asynchronous code in a synchronous way. We will talk about this later in this article.
        
        Overall, the Coroutines make the multitasking very easy.
        
        ```kotlin
        fun functionA(case: Int) {
            when (case) {
                1 -> {
                    taskA1()
                    functionB(1)
                }
                2 -> {
                    taskA2()
                    functionB(2)
                }
                3 -> {
                    taskA3()
                    functionB(3)
                }
                4 -> {
                    taskA4()
                    functionB(4)
                }
            }
        }
        
        fun functionB(case: Int) {
            when (case) {
                1 -> {
                    taskB1()
                    functionA(2)
                }
                2 -> {
                    taskB2()
                    functionA(3)
                }
                3 -> {
                    taskB3()
                    functionA(4)
                }
                4 -> {
                    taskB4()
                }
            }
        }
        ```
