<h1>Arrays</h1>
Arrays is a container which hold a fixed number of values in a single type. Arrays are represented by class called *java.util.Arrays..*

***Advantages*** :- 

- It's based on index collections and stored in memory from left to right.
- Default value of array is "0" in primitives, "null" in objects, "false" in boolean.
- It's size is fixed and we can represent multiple values under the same name. So that readability of code is improved.

***Disadvantages*** :- size of an array are fixed. 

- As array is homogenous datastructure so it can store only unifomed elements.

How to create java array?

- Declaring array variable and initialize an array object.

```kotlin
int array[];     // Declaring
array = new int[10];     // Initializing
```

Types of an Java Array

1. Single Dimensional Arrays    2. Multidimensional arrays    3. Anonymous arrays

1. ***Single dimensional arrays*** :- Ever array is an object. so that we can create an array using new operator.

`int[] a = new int[10];`

```java
int[] a = new int[10];
int[] a = {5,10,60,50,70};
----------------------------------------------------------------------------------------int[] a = new int[];  // Compilation Error
int[] a = new int[-1];  // Runtime Exception (NegativeArraySizeException)
int[] a = new int[10];   // Legal
```

![Arrays.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c30cfb2-f752-4dbe-ae4d-4dcfbed9103f/Arrays.png)

1. ***Java Multidimensional Arrays*** :- It's noting but Arrays of array. Main use of this is memory utilization will be improved. 
    
    ![MultidimentionalArray1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65e1cafe-5c31-4a1b-88f7-0501bcfc8d98/MultidimentionalArray1.png)
    

Arrays Single Line Declaration, Initialization

`int[][] a={{1,5,6,7,},{10,20,30}};` // you need to perform declaration, initialization in one line otherwise Compiler will generate an exception.

```java
int[] x;
x={10,20,30};  // Illegal State Exception
```

1. ***Java Anonymous Arrays*** :- in this anonymous we can specify the size. Otherwise we will get compilation error. 
    
    `new int[]{5,10,15,20,25};`
    
    ---
    
    ---
    

Arrays is the Data Structure used to hole homogenous element at contiguous locations.

One memory block is allocated for the entire array to hold the elements of the array. The array elements can be accessed in constant time by using the index of the particular element as the subscript.

:- Explanation: let's take an example if an integer is takes 2 bytes. if my first element stores at 1000 address then then second element will be stored at 1002 address in the memory. similarly third element stored at 1004 address.
