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
