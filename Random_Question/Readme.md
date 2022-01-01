- Launch Mode's android
    1. Standard ⇒ whenever we launch the new activity it will just added to the stack or task. If that activity is still present inside the stack then also it will create a new intance and add it to the stack.
    2. SingleTop ⇒ In this launch mode we add activity a and and above it we added avtivity b and then again try to add activity b then it will not create new instance of that activity. and stack size will remain same. ( if activity is on top of the stack don't create new instance  )
    
    ---
    
    1. SingleTask ⇒ 
        1. With taskAffinity → it will create one more task or stack
            1. New Activity would be launched at root of the new task
            2. From now on any activities triggered from 'b" would be part of 'B' task
            3. If 'B' triggered itself, then no new instance is created and existing instance in existing task will re-used.
            4. If 'B' instance already exists(in any takss), it will be reused
            5. If 'B' in the single activity in task, it will be just brought to foreground.
            
            1. If other activities are present on 'B' they will be popped and then the task will be brought to foreground.
            
            Single task activity will always be at root of task.
            
            There can only be one singleTask activity across tasks.
            
        2. without task Affinity
            1. here affinity b is not launched in the seperate  task
            
            Single task activity need not to be root of the task.
            
            Single Task activity will not be launched in new task.
            
            There can only be one 'single Task activity across tasks.
            
    2. SingleInstance ⇒ 
        
        Activity A→ added activity B create new Task, Activity C → Activity D.
        
        Activity B →  
        
        here if you declate the task affinity the you can easily switch between them that's the advatage.
        
        Single Instance will always be at the root of new task
        
        No other activity can be part of task containing SingleInstance activity
        
    
    What if we want to control launch mode in runtime? Manifest file is not editable at run time?
    
    1. Using  the IntentFlags you can control the launch mode's of an activity at the run Time.
    
    ```kotlin
    val intent = Intent(this,targetActivity::class.java)
    intent.flags= Intent.FLAG_ACTIVITY_NEW_TASK
    intent.flags= Intent.FLAG_ACTIVITY_CLEAR_TOP //there is no launch mode for this
    intent.flags= Intent.FLAG_ACTIVITY_SINGLE_TOP
    startActivity(intent)
    ```
    
- Android Application component
    
    App components are the essential building blocks of an Android app. Each component is an entry point through which the system or a user can enter your app
    
    - Activity
        1. Represent the visual representation of the android application.
        2. An activity is the entry point for interacting with the user. It represent the single screen with a user interface.
        3. it keep the track what user currently cares about to ensure that the system keeps running the process that is hosting the activity.
    - Services
        - A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.
        - This component runs in the background to perform long-running operations. A service does not provide a user-interface.
        - They have their own lifecycler independent of the activity or fragmetn that they were created in.
        - By default services work on a main thread.
        - TYPES:- Their are two types of service that tell the system how to manage an app
            
            A bound service can also be a started service but a started service can not be a bound service 
            
            - Started Service
                
                It startd up by calling "startService" or "starForegroundService"
                
                - Tells the system to keep them running until thier work is completed. This could be to sync some data in the background or play music even after the user leaves the app.
                - Types 1. Foreground (notify the user )2. Background ( don't notify the user )
            - Bound Service
                
                ![https://www.tutorialspoint.com/android/images/services.jpg](https://www.tutorialspoint.com/android/images/services.jpg)
                
                Communicate with it on a consistent bases. By Binding to it, you can communicate with the service very easily.
                
                you can start this service in 2 different ways.
                
                1. When some other component binds to it literal act of a something binding to it.
                2. startService or startForegroundService and then Bind to it.
                
                Bound service is something like a server. where it will start a server, and bind to it with some kind of client. 
                
                You define it to a Client-server Interaction where there service act as the server and component act as a client. Client could be an activity a fragment or watch or other application.
                
                If their is a consistent or frequent communication between some client and the service e.g Streaming service.
                
    - Broadcast Receivers
        - Broadcast receiver is nothing but basically it's a listener which will listen all the events happened into the application ( here events are Battery low, incomming call, incomming sms, wifi-availability etc ) as we got these event as a Intent so when device matches the event will triggered the events. Broadcast Receiver should register in the Manifest to listen this event's and its registered properly then it will respond properly through intent.
    - Content Providers
        1. Content Providers:- An object used to work with data via content providers. your application can share data with other applicatoins. Content provider have the SQL lite database and it's work on this.
        2. :- Perform an action in response to a message from some other component. Broadcast receiver fires and intent and says this thing comes us.
    
- What is fragment
    
    Android Fragment is **the part of activity**, it is also known as sub-activity. There can be more than one fragment in an activity. Fragments represent multiple screen inside one activity. Android fragment lifecycle is affected by activity lifecycle because fragments are included in activity.
    
- What's the difference between commit() and commitNow()
    
    Like commit but allows the commit to be executed after an activity state is saved. But it's dangerous as the commit can be lost if acitivty needs to be restored later from it's state.
    
    So should be used at the cases where it's ok of Ui state chages unexpectdly.
    
- **onSavedInstanceState() and onRestoreInstanceState() in activity**
    
    Before screen is rotatd whatever data we had we save it using onSavedInstace function and after screen get rotated to get the same data we use onRestoreInstanceState.
    
    - onSavedInstanceState() - This method is used to store data before pausing the activity. and it will store using outstate(key,value)
    - onRestoreInstanceState() - This method is used to recover the saved state of an activity when the activity is recreated after destruction. So, the onRestoreInstanceState() receive the bundle that contains the instance state information. we can get the details by using savedInstanceState.get(key , Default value ) and assign to the value
- Content Provider
    
    Using content provider we can share data in the secured manner. app2 will use the api request called content resolver using which it will hit app1 database or data. And Content provider which is in app1 will respond back using cursor. It's the interprocess communication.
    
    getContentResolver() return instance of the content resolver
    
    URI → path
    
    n the content provider we get the repsonse in the tabular format.
    
    ---
    
    ---
    
    - The role of the content provider in the android system is like a central repository in which data of the applications are stored, and it facilitates other applications to securely access and modifies that data based on the user requirements
    - **Content URI(Uniform Resource Identifier)** is the key concept of Content providers. To access the data from a content provider, URI is used as a query string.
    
    ### **Operations in Content Provider**
    
    Four fundamental operations are possible in Content Provider namely **Create**, **Read**, **Update**, and **Delete**. These operations are often termed as **CRUD operations**.
    
    - **Create:** Operation to create data in a content provider.
    - **Read:** Used to fetch data from a content provider.
    - **Update:** To modify existing data.
    - **Delete:** To remove existing data from the storage.
    
    ### **Working of the Content Provider**
    
    UI components of android applications like **[Activity](https://www.geeksforgeeks.org/activity-lifecycle-in-android-with-demo-app/)** and **[Fragments](https://www.geeksforgeeks.org/introduction-fragments-android/)** use an oject **CursorLoader** to send query requests to **ContentResolver.** The ContentResolver object sends requests (like create, read, update, and delete) to the **ContentProvider** as a client. After receiving a request, ContentProvider process it and returns the desired result. 
    
- **Does a service run in the background thread**
    
    A service runs **in the main thread of its hosting process**; the service does not create its own thread and does not run in a separate process unless you specify otherwise. You should run any blocking operations on a separate thread within the service to avoid Application Not Responding (ANR) errors.
    
- **What are broadcast receivers**
    
    Broadcast Receivers simply respond to broadcast messages from other applications or from the system itself. These messages are sometimes called events. For example, applications can also initiate broadcasts to let other applications know that some data has been downloaded to the device and is available for them to use, so this is the broadcast receiver who will intercept this communication and will initiate appropriate action.
    
    - Normal Broadcast
        - Declaring Broadcast in the manifest file will work in the various situation but in certain cinario it's not an appropriate solution.
            - For E.g Assume you had to read OTP from msg which had been sent on your device. It's work is to read it and recognise the incomming OTP but if app is not in forgroud in that app will receive the OTP as it is declared in the manifest file which is wrong. Instead of declaring it in the manifest declare in the code.
                
                `IntentFiller filter = new IntentFilter("android.provider.Telephony.SMS_RECEIVED")`
                
            - In this case register in onStart() and unregister() on onPause() methods.
        - My custom Event :-
            
            ```kotlin
            val intent = Intent()
            
            intent.addCategory(Intent.CATEGORY_DEFAULT)
            
            intent.action= "my.custom.action.tag.fordemo"
            
            sendBroadcast(intent)
            ```
            
        - How to secure BR?
        
        → Here the problem is if any app knows the action can trigger the broadcast but what if you don't know the action? for that you can make use of the attibute called `android:exported = "false"` 
        
        - How to prevent intent Broadcast propagation ? ( colision of BR when both actions are same) ?
        
        → Suppose you have 4 app with same action and category values `app1`, `app x`, `app y`, `app z`
        
        and if Broadcast event happen then all the broadcast event will triggered, if you don't want that to happened then use LocalBroadcastManager to send the broadcast. So this case it will propogate to `app x` only not other app .
        
    - Ordered Broadcast
        - Can we control the order in which broadcasr Receivers get Triggered ? Like firstly `app1` Broadcast should triggered then , `app x`, then  `app y`, and finally `app z` ?
            
            → The answer is Yes using Ordered Broadcast Receiver's.  
            
            Here you can use the attribute in the intent-filter called `android:priority="1"` ( higher the number higher the priority.
            
            - For sending in ordered you can change the broadcast of `sendBroadcast(intent)` use `sendOrderedBroadcast(intent,null)` here if you need the permission then you can write permission else write null.
            - Using `BREAD_CRUMB` you can fetch the previous value and send to the next BroadCast.
    - The Finer Nuances
        - It runs on the Main thread/Ui Thread, `(can lead to ANR)`
            - Android suggest that BR should not do anything which takes more than 10 sec.
        - BR is considered to be finished after onReceive()
            - BR is not suited for asynchronous calls
            - Never bind to a service from BR
            - However you can start a Service from BR
        - BR are prone to hacks, thus always secure them.
            - set exported attribute to false
            - use localBroadcastManager to limit propagation beyond app.
- How to use Broadcast
    
    The Whole process of using a broadCast divided into two parts
    
    - Register Broadcast → For register broadcast into the application you had 2 options. Either you can register the event in the AndroidManifest.xml file of application or you can register broadcast via the Context.registerReceiver() method ( programatically ).
    - Receive Broadcast → By extending the BroadcastReceiver abstract class, you can receive the broadcast in your application. After extending, all you need to do is override the **onReceive()** method and perform the required action in the **onReceive()** method because this onReceive() method will be called when a particular broadcast is received.
- What is LocalBroadcastManager in Android
    - If the communication is not between different applications on the Android device then it is suggested not to use the Global BroadcastManager because there can be some security holes while using Global Broadcastmanager and you don’t have to worry about this if you are using LocalBroadcastManager.
    - LocalBroadcastManager is used to register and send a broadcast of intents to local objects in your process. It has lots of advantages:
        1. Broadcasting data will not leave your app. So, if there is some leakage in your app then you need not worry about that.
        2. Another thing that can be noted here is that other applications can’t send any kind of broadcasts to your app. So, you need not worry about security holes.
    - How you can use it ?
        
        ```kotlin
        /*
        To use LocalBroadcastReceiver, all you need to do is create an instance of LocalBroadcastManager, then send the broadcast and finally receive the broadcast. So, firstly, create an instance of the LocalBroadcastManager:
         */
        
        var localBroadcastManager = LocalBroadcastManager.getInstance(context)
        Now, by using the sendBroadcast() method, you can send the broadcast as below:
        
        val localIntent = Intent("YOUR_ACTION")
            .putExtra("DATA", "Aditya")
        localBroadcastManager.sendBroadcast(localIntent)
        /*
        Our final task is to receive the broadcast using the onReceive() method on MyBroadCastReceiver. You can perform the desired action after receiving the broadcast in the onReceive() method as below:
         */
        
        private val listener = MyBroadcastReceiver()
        
        inner class MyBroadcastReceiver : BroadcastReceiver() {
            override fun onReceive(context: Context, intent: Intent){
                when (intent.action) {
                    "YOUR_ACTION" -> {
                        val data = intent.getStringExtra("DATA")
                        Log.d("Your Received data : ", data)
                    }
                    else -> Toast.makeText(context, "Action Not Found", Toast.LENGTH_LONG).show()
                }
        
            }
        }
        /*
        Now, this will print an output in Logcat,
         */
        
        Your Received data : Aditya
        ```
        
- Service and Type of Service
    - Depth
        
        ```java
         * To Start the service you had to write in into manifest.
         * YOu cannot stop a service thier is no explicit way to stop the service.
         * Service always run on the main thread. If you are performing long running operation then you had to create a bg Thread.
         * To Stop the service you can use stop Self
         *
         Service Behaviour
            * What Happen to the app when resource crunch situation arises?
            -> If you are running so many application then android may kill your previous app in case that app contain service running in bg then andriod
                will not try to kill the app as the service get the high priority. if Resouce is soo serious the it will close the app.
        
            * What Should happened to the service which has been killed?
            -> That is determined the value you wrote in the onStartCommand
                * weather you had to restart the service and restarted service had the intent value populated so that it can continue with it's work.
                * If integer constant is START_STICK -> autoRestart 'Yes' when resources available but intent will be 'Null Intent'
                * If integer constant is START_NOT_STICK -> autoRestart 'No' that doesn't mean service will not start at all if you triggere the intent to start the service again the it will start and when resources available but intent 'With Intent when started'
                * If integer constant is START_REDELIVER_INTENT -> autoRestart always 'Yes' when resources available but intent 'Intent'
        
            * START_SERVICE -> Service are being explicitly managed & long running
                            -> no need to remember state at kill time
                            -> long running music playing service
        
            * START_NOT_STICKY -> Service are being not explicitly managed
                               -> Services are periodically running and self stopping
                               -> Alarm service or server data polling
        
            * START_REDELIVER_INTENT -> Service are being explicitly managed
                                     -> Restart from previous state at the kill time
                                     -> File Download
        
         * Quick Intro To Bound Service
         * 'BOUND_SERVICE' -> A Service which is providing an information to Activity or the bound service is known as 'BOUND_SERVICE'
         * 'LOCAL_BINDING' -> Component which are establishing the connection or binding between service to service or service to activity of the same app that's why we called it as 'LOCAL_BINDING'
                Local Binding Implementation -> IBinder
         * 'REMOTE_BINDING' -> Component which are establishing the connection or binding between service to service or service to activity of the two different app's that's why we called it as 'REMOTE_BINDING' or IPC(inter-process-communication)
                Remote Binding Implementation -> Messenger API and AIDL(Android Interface definition language)
                                              -> Messenger -> it's basically a queued concept where every component which want to connect to the service will trigger a request that are queued i.e they are more suited for non multithreaded scenario
                                              -> AIDL -> it's basically highly concept and they are more suited for multithreaded environment. Official Document say's most application should not used AIDL.
        
         * Local Binding Implementation -> Implement onBind which return IBinder instance
                                        -> Use ServiceConnection API to Connect To service
        
        ```
        
    
    A service is a component which runs in the background to perform certain tasks or long-running operations without needing to interact with the user. And it works even if the application is destroyed. Using Service you can perform InterProcess Communication (IPC)
    
    Types:-
    
    1. Foreground/UnBound Service :- A service is start when an application compoent such as activity, starts it by calling startService(). Once started a service can run in the background even the component or activity that started is destroyed.
    2. Background :- Here user will never know about what is happening in the background of the application. For example while sending some images over whatsapp, it compresses the image file to reduce the size. Here the task is done in the background and the user had no idea about it.
    3. Bound service :- A service is bound when one or more  application component binds to it by calling bindService(). offers client-server interface that allows component interact with service, send request, get result and even do IPC(inter process communication).
    
    return START_STICKY → it will run untill I explicitly call stop method
    
    return START_NONSTICKY → it will run and finish once it's work is done
    
    Lifecycle :- 
    
    onCreate → onStatCommand → onBind →onUnBind → onRebind → onDestroy
    
    ![https://www.tutorialspoint.com/android/images/services.jpg](https://www.tutorialspoint.com/android/images/services.jpg)
    
- **Different ways to communicate between service and activity/fragments**
    1. You can use Bound Service which acts as a server in client-server interface.
    2. You can use Broadcast Receiver
    3. You can use Bus Architecture
    4. You can used Result Receiver
- What is Service, IntentService and JobIntentService
    - Service - This runs on the same main thread which invokes this service and performs some background operation. For any long running operation happening on the main thread it is recommended to create a new thread and do the job (eg; `Handler`) by not impacting the main thread's performance.
        
        **Drawback : Runs on main thread**
        
    - IntentService - Intent service also helps in doing some long running (indefinite) background task. The only difference is that it creates a new thread to perform this task and does not run on the main thread. Does the given job on it's `onHandleIntent`.
        
        **Drawback: The job given to the IntentService would get lost when the application is killed**
        
    - JobIntentService - Job intent service is very similar to IntentService but with few benefits like the application can kill this job at any time and it can start the job from the beginning once the application gets recreated/up.
    
    But from Oreo, if the app is running in background it's not allowed to start the service in background. Android asks us to start the service explicitly by `context.startForegroundService` instead of `context.startService` and when the service is started within 5 seconds it must be tied to the notification to have a UI element associated with it.
    
- **What is the difference when you extend a class with service and IntentService**
    1. **Usage:** If you want some background task to be performed for a very long period of time, then you should use the IntentService. But at the same time, you should take care that there is no or very less communication with the main thread. If the communication is required then you can use main thread handler or broadcast intents. You can use Service for the tasks that don’t require any UI and also it is not a very long running task.
    2. **How to start?:** To start a Service you need to call the **onStartService()** method while in order to start a start IntentService you have to use Intent i.e. start the IntentService by calling **Context.startService(Intent).**
    3. **Running Thread:** Service always runs on the **Main thread** while the IntentService runs on a separate **Worker thread** that is triggered from the Main thread.
    4. **Triggering Thread:** Service can be triggered from any thread while the IntentService can be triggered only from the Main thread i.e. firstly, the Intent is received on the Main thread and after that, the Worker thread will be executed.
    5. **Main Thread blocking:** If you are using Service then there are chances that your Main thread will be blocked because Service runs on the Main thread. But, in case of IntentService, there is no involvement of the Main thread. Here, the tasks are performed in the form of Queue i.e. on the First Come First Serve basis.
    6. **Stop Service:** If you are using Service, then you have to stop the Service after using it otherwise the Service will be there for an infinite period of time i.e. until your phone is in normal state. So, to stop a Service you have to use **stopService()** or **stopSelf()**. But in the case of IntentService, there is no need of stopping the Service because the Service will be automatically stopped once the work is done.
    7. **Interaction with the UI:** If you are using IntentService, then you will find it difficult to interact with the UI of the application. If you want to out some result of the IntentService in your UI, then you have to take help of some Activity.
- What is JobScheduler
    
    This is an API for scheduling various type of jobs against the framework that will be executed in your applicaiton's own process.
    
    When the criteria declared are met, the system will execute this job on your application's `[JobService](https://developer.android.com/reference/android/app/job/JobService)`
    
    For more details refer this :- [LINK](https://medium.com/@kiitvishal89/android-jobscheduler-schedule-your-jobs-like-a-master-cfa0d80e5f10)
    
- Thread
    1. Thread cannot directly put the task in the queue. for that we use Handler 
    2. Thread → handler ( will have the reference of message queue) → send runnable instance → messageQueue
    
    handler.post() //setting the text.
    
- AsyncTask
    
    It's basically an api which has for methods. These 4 task will help you to perform long running operation in such a way that you don't disturb the main thread.
    
    1. onPreExecute() → executed on the main thread, can do any kind of initiazlization
    2. onPostExecute() → executed on the main thread, updates the ui when work is done 
    3. doInBackground() → run's on the backgroun thread
    4. onProgressUpdate() → provides the progress of the work.
    
    AsyncTask is designed to be a helper class around `[Thread](https://developer.android.com/reference/java/lang/Thread)` and `[Handler](https://developer.android.com/reference/android/os/Handler)` and does not constitute a generic threading framework. AsyncTasks should ideally be used for short operations (a few seconds at the most.) If you need to keep threads running for long periods of time, it is highly recommended you use the various APIs provided by the `java.util.concurrent` package such as `[Executor](https://developer.android.com/reference/java/util/concurrent/Executor)`, `[ThreadPoolExecutor](https://developer.android.com/reference/java/util/concurrent/ThreadPoolExecutor)` and `[FutureTask](https://developer.android.com/reference/java/util/concurrent/FutureTask)`.
    
    An asynchronous task is defined by a computation that runs on a background thread and whose result is published on the UI thread. An asynchronous task is defined by 3 generic types, called `Params`, `Progress` and `Result`, and 4 steps, called `onPreExecute`, `doInBackground`, `onProgressUpdate` and `onPostExecute`.
    
    Android AsyncTask going to do background operation on background thread and update on main thread. In android we cant directly touch background thread to main thread in android development. asynctask help us to make communication between background thread to main thread.
    
- **What are handlers**
    
    A Handler allows you to send and process `[Message](https://developer.android.com/reference/android/os/Message)` and Runnable objects associated with a thread's `[MessageQueue](https://developer.android.com/reference/android/os/MessageQueue)`. Each Handler instance is associated with a single thread and that thread's message queue. When you create a new Handler it is bound to a `[Looper](https://developer.android.com/reference/android/os/Looper)`. It will deliver messages and runnables to that Looper's message queue and execute them on that Looper's thread.
    
    There are two main uses for a Handler: 
    
    1.  To schedule messages and runnables to be executed at some point in the future
    2.  to enqueue an action to be performed on a different thread than your own.
    
    How TO schedule ?
    
    Scheduling messages is accomplished with the post(Runnable), postAtTime(Runnable, long), postDelayed(Runnable, long), sendEmptyMessage(int), sendMessage(Message), sendMessageAtTime(Message, long), and sendMessageDelayed(Message, long) methods.
    
- **What are Loopers**
    
    **Simplest Definition of Looper & Handler:**
    
    *Looper* is a class that turns a thread into a **Pipeline Thread** and *Handler* gives you a mechanism to push tasks into this pipe from any other threads.
    
    **Details in general wording:**
    
    So a **PipeLine Thread** is a thread which can accept more tasks from other threads through a Handler. 
    
    The **Looper** is named so because it implements the loop – takes the next task, executes it, then takes the next one and so on. The Handler is called a handler because it is used to handle or accept that next task each time from any other thread and pass to Looper (Thread or PipeLine Thread).
    
    **Need Of Looper:** 
    
    1. To keep the thread active solve issue of thread getting destroyed after executing runnable method.
    2. If someone wants to execute multiple messages(Runnable) then he should use the Looper class which is responsible for creating a queue in the thread.
    
    **Example:**
    
    A Looper and Handler or PipeLine Thread's very perfect example is to download more than one images or upload them to a server (Http) one by one in a single thread instead of starting a new Thread for each network call in the background.
    
- **What is a Message-Queue**
    
    Low-level class holding the list of messages to be dispatched by a Looper. Messages are not added directly to a MessageQueue, but rather through Handler objects associated with the Looper. MessageQueue is a message loop or message queue which basically contains a list of Messages or Runnables (set of executable code).
    
- **Difference between Serializable and Parceable**
    
    In Android, we cannot just pass objects to activities. To do this the objects must either implement `Serializable` or `Parcelable` interface.
    
    **Serializable**
    
    `Serializable` is a standard Java interface. You can just implement `Serializable` interface and add override methods. The problem with this approach is that reflection is used and it is a slow process. This method creates a lot of temporary objects and causes quite a bit of garbage collection. However, `Serializable` interface is easier to implement.
    
    Serializable is a standard Java interface. You simply mark a class Serializable by implementing the interface, and Java will automatically serialize it in certain situations.
    
    **Parcelable**
    
    `Parcelable` process is much faster than `Serializable`. One of the reasons for this is that we are being explicit about the serialization process instead of using reflection to infer it. It also stands to reason that the code has been heavily optimized for this purpose.
    
    Parcelable is an Android-specific interface where you implement the serialization yourself. It was created to be far more efficient than Serializable, and to get around some problems with the default Java serialization scheme.
    
    Parcelable is a better choice since it is recommended by Google.
    
- **How would you update the UI from the background thread**
    
    Although using ‘onPostExecute’ in an ‘AsyncTask’ is one of the solutions, that cannot be applied everywhere, especially where there is no Async Task (eg. when you are making an asynchronous network call with the help of a third party library). Wrapping up a **synchronous** network call with **Async Task** is one of the ways of using the AsyncTask.
    
    I recently encountered the same problem when I wanted to make an **asynchronous** call using HttpOk library and then I came to know about this…
    
    [https://qphs.fs.quoracdn.net/main-qimg-a620f83f23dd32685988b07c1e15efb4](https://qphs.fs.quoracdn.net/main-qimg-a620f83f23dd32685988b07c1e15efb4)
    
    We make a new **runnable** in something called **runOnUiThread()**. Then, we tell the system to run particular lines of code on the UI thread. The syntax is shown above. Instead of MainActivity.class, the actual Activity name should be used, and in the run() function, you can mention the code you want to be executed in the UI thread.
    
    You can insert the above bit of code in the location where you want the actions to be performed on the main UI thread.
    
- **What is the intent? What is the` maximum amount of data that you can transfer using intent**
    - An intent is a messaging object you can use to request an action from another app component.
    - Using Intent you can start an activity, start a service, delivering broadcast.
    - The maximum amount of data transfer is approx 1MB
- What is a fragment
    - Fragment is a small chunk of UI
    - It has it's own lifecycle
    - it can process it's own events
    - it can be added or removed which the activity runs
- **When should you use a fragment rather than Activity**
    - Combines several fragment in a single activity.
    - Reuse the same fragment across several activities
    - Make better use of larger screen space tablets
    - Support different layouts on portrait and landscape modes
    - Fixed/Scrolling/Swipe tab displays
    - Dialog Boxes
    - Action bar customization with the list and tab modes
- **Why is it recommended to use a default constructor while creating a fragment**
    - Android framework decides to recreate our fragment when the orientation changes. Android calls the no-argument constructur of our fragment. It has no idea what constructor we have created.
    - fragment.argument = bundle →  in the newInstance we are passing the bundle inside it. so when we create a newInstance android will extract the bundle and store it. so when android orientation changes the android will recreates fragment using the no-arguemnt construtor and
    - can attach the bundle to the fragment as it has stored the bundle earlier. and later we can again accss that data by using getArgument like ( val video_id = argument?.getLong(EXTRA_VIDEO_ID )
    - So system restores  a Fragment
    - It will automatically restore our bundle
    - Restore the state of the fragment to the same state.
- **What is Context**
    - Defination
        - It is the context of the current state of the application, used to get information regarding activity and applciation, can be used to get access to resources, databases and shared preferences and both activity and application class extend context.
    - Literal meaning of context is:
    
    > The circumstances that form the setting for an event, statement, or idea, and in terms of which it can be fully understood
    > 
    - The context tells us about the surrounding information.
    - It is very important to understand the environment which we want to understand.
    
    > Android Programming context can be understood as something which gives us the context of the current state of our application. We can break the context and its use into three major points
    > 
    - It allows us to access resources.
    - It allows us to interact with other Android components by sending messages.
    - It gives you information about your app environment.
    
    ---
    
    *Interface to global information about an application environment. This is an abstract class whose implementation is provided by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level operations such as launching activities, broadcasting and receiving intents, etc.*
    
    ---
    
    ***Understanding Context by a Real World Example***
    
    *Let’s a person visit a hotel. He needs breakfast, lunch, and dinner at a suitable time. Except for these things there are also many other things, he wants to do during the time of stay. So how does he get these things? He will ask the room-service person to bring these things for him. Right? So here the **room-service person is the context** considering **you are the single activity** and **the hotel to be your app**, finally, the **breakfast, lunch & dinner have to be the resources**.*
    
    **How Does It Work**
    
    1. It is the context of the current/active state of the application.
    2. It is used to get information about the activity and application.
    3. It is used to get access to resources, databases and shared preferences etc.
    4. Both the activity and application classes exent the context class. 
    
    ***Types of Context :- Application Context and Activity Context***
    
- **What is Application Context**
    - It is the application and we are present in Application. For example - MyApplication(which extends Application class). It is an instance of MyApplication only.
    - Both the Activity and Application classes extend the Context class.
    - It is an instance that is the singleton and can be accessed in activity via `getApplicationContext()`. This context is tied to the lifecycle of an application. The application context can be used where you need a context whose lifecycle is separate from the current context or when you are passing a context beyond the scope of activity.
    - Example Use: If you have to create a singleton object for your application and that object needs a context, always pass the application context.
    - If you pass the activity context here, it will lead to the memory leak as it will keep the reference to the activity and activity will not be garbage collected.
    - In case, when you have to initialize a library in an activity, always pass the application context, **not** **the activity context**.
    - You only use `getApplicationContext()` when you know you need a `Context` for something that may live longer than any other likely `Context` you have at your disposal.
    - Wrong use of Context can easily lead to memory leaks in an android application
- **What is Activity Context**
    - This context is available in an activity. This context is tied to the lifecycle of an activity. The activity context should be used when you are passing the context in the scope of an activity or you need the context whose lifecycle is attached to the current context.
    - Example Use: If you have to create an object whose lifecycle is attached to an activity, you can use the activity context.
    
    The app hierarchy looks like the following:
    
    ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/context-app-activity-hierarchy.jpg](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/context-app-activity-hierarchy.jpg)
    
    - MyApplication [Here we have only Application context present] [Nearest Context is Application Context]
    - MainActivity1 [Here we have both Activity(MainActivity1) context and Application context present] [Nearest Context is Activity Context]
    - MainActivity2 [Here we have both Activity(MainActivity2) context and Application context present] [Nearest Context is Activity Context]
    - It returns the Context which is linked to the Activity from which it is called. This is useful when we want to call the context from only the current running activity. and it can be used for toast, intent start activity
- **When to use Context and Application context**
    
    Let's learn which context to use at which place with an example:
    
    - Suppose we have our class MyApplication(which extends the Application class). And, another class MyDB which is Singleton. And MyDB(which is Singleton) needs context. Which context will we be passing?
    - The answer is Application Context because if we pass the Activity Context (for example MainActivity1), even if MainActivity1 is not in use, the MyDB will be keeping the reference unnecessary which will lead to the memory leaks.
    - So always remember, in case of Singleton(lifecycle is attached to the application lifecycle), always use the Application Context.
    - So, now when to use the Activity Context. Whenever you are in Activity, for any UI operations like showing toast, dialogs, and etc, use the Activity Context.
    - Always try to use the nearest context which is available to you. When you are in Activity, the nearest context is Activity context. When you are in Application, the nearest context is the Application context. If Singleton, use the Application Context
- **When to not to use Application context**
    - It’s not a complete `Context`, supporting everything that `Activity` does. Various things you will try to do with this `Context` will fail, mostly related to the GUI.
    - It can create memory leaks if the `Context` from `getApplicationContext()` holds onto something created by your calls on it that you don’t clean up. With an `Activity`, if it holds onto something, once the `Activity` gets garbage collected, everything else flushes out too. The `Application` object remains for the lifetime of your process.
- **What is the lifecycle of a View**
    
    # **View Life Cycle**
    
    Every Activity has it’s own life cycle similarly Views also have a Life Cycle. A view which was rendered on the screen must undergo these lifecycle methods to get drawn on the screen correctly. Each of these methods has its importance. Let’s dive into the life cycle.
    
    [https://miro.medium.com/max/875/0*cHmlPwPvhWJ15zU3](https://miro.medium.com/max/875/0*cHmlPwPvhWJ15zU3)
    
    ### **Constructors**
    
    Usually, we get confused about why there are four types of constructors for a View
    
    ```
    View(Context context) View(Context context, @Nullable AttributeSet attrs) View(Context context, @Nullable AttributeSet attrs, int defStyleAttr) View(Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes)
    ```
    
- What happens when you make an API request on UI thread
    - Making api request on UI thread will basically block the Ui component's as it's happen synchronously due with Ui will reaming completely unreponsive untill operation completes. for this reason you should use the seperate threads which thereby avoid blocking the Ui.
- **What are the differences between Thread & Async tasks**
    
    # Thread
    
    A thread is a concurrent unit of execution. It has its own call stack. There are two methods to implement threads in applications.
    
    1. One is providing a new class that extends Thread and overriding it's run() method.
    2. The other is providing a new Thread instance with a Runnable object during its creation.
    
    A thread can be executed by calling its "start" method. You can set the "Priority" of a thread by calling its "setPriority(int)" method.
    
    A thread can be used if you have no effect in the UI part. For example, you are calling some web service or download some data, and after download, you are displaying it to your screen. Then you need to use a Handler with a Thread and this will make your application complicated to handle all the responses from Threads.
    
    A Handler allows you to send and process Message and Runnable objects associated with a thread's MessageQueue. Each thread has each message queue. (Like a To do List), and the thread will take each message and process it until the message queue is empty. So, when the Handler communicates, it just gives a message to the caller thread and it will wait to process.
    
    If you use Java threads then you need to handle the following requirements in your own code:
    
    - Synchronization with the main thread if you post back results to the user interface
    - No default for canceling the thread
    - No default thread pooling
    - No default for handling configuration changes in Android
    
    # AsyncTask
    
    AsyncTask enables proper and easy use of the UI thread. This class allows performing background operations and publishing results on the UI thread without having to manipulate threads and/or handlers. An asynchronous task is defined by a computation that runs on a background thread and whose result is published on the UI thread.
    
    AsyncTask will go through the following 4 stages:
    
    1. **onPreExecute()**Invoked on the UI thread before the task is executed
    2. **doInbackground(Params..)**Invoked on the background thread immediately after onPreExecute() finishes executing.
    3. **onProgressUpdate(Progress..)**Invoked on the UI thread after a call to publishProgress(Progress...).
    4. **onPostExecute(Result)**Invoked on the UI thread after the background computation finishes.
- what is singleton
    
    a singleton class is a class that can have only one object
    
    so we cannot create an instance of the singleton class.
    
    if we had non-singleton class and if we have initialize it everytime then each time we had to create a new object of that class and address of that class will be different each time. but in case of singleton class address remains the same.
    
- **What is the difference between commit and apply in sharedpreferences**
    
    the differences of commit() and apply().
    
    1. Return value:
    
    ```kotlin
    apply() commits without returning a boolean indicating success or failure.commit()  returns true if the save works,false otherwise.
    ```
    
    2. Speed:
    
    ```kotlin
    apply() isfaster.commit() isslower.
    ```
    
    3. Asynchronous v.s. Synchronous:
    
    ```
    apply():Asynchronous commit():Synchronous
    ```
    
    4. Atomic:
    
    ```
    apply(): atomic commit(): atomic
    ```
    
    5. Error notification:
    
    ```
    apply():No commit():Yes
    ```
    
- **What is a recycler view and How does it work**
    
    ## **What is RecyclerView?**
    
    RecyclerView is a ViewGroup, which populates a list on a collection of data provided with the help of ViewHolder and draws it to the user on-screen.
    
    ### **Building components of RecyclerView**
    
    The major components of RecyclerView are,
    
    - Adapter
    - ViewHolder
    - LayoutManager
    
    ### **Adapter**
    
    It is a subtype of RecyclerView.Adapter class. It takes the data set which has to be displayed to the user in RecyclerView. It is like the main responsible class to bind the views and display it.
    
    Most of the tasks happen inside the adapter class of the recyclerView.
    
    ### **ViewHolder**
    
    ViewHolder is a type of a helper class that helps us to draw the UI for individual items that we want to draw on the screen.
    
    All the binding of Views of the individual items happens in this class. It is a subclass of RecyclerView.ViewHolder class.
    
    ### **LayoutManager**
    
    LayoutManager in recyclerView helps us to figure out how we need to display the items on the screen. It can be linearly or in a grid. RecyclerView provides by default a few implementations of layoutManager out of the box.
    
    It is like the governing body of recyclerView which tells the recyclerView's adapter when to create a new view.
    
    ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/relation-rcv-29094a550bfcc3d8.jpg](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/relation-rcv-29094a550bfcc3d8.jpg)
    
    ### **How it actually works?**
    
    So, now we are going to discuss how the recyclerView actually works. When we talk about recyclerView, you would always hear someone saying that it **recycles** the views. But what does it actually mean?
    
    So, let's say when we are scrolling the list which has **50 items** in the collection and we show only **5 items** at once in the list like,
    
    Here, **item 1** to **item 5** is the ones that are visible on the screen. `item x` is the one that will be loaded next on the screen when we scroll up.
    
    All the items here have their own instance of ViewHolder and the ViewHolder here is helpful for caching the specific item's view.
    
    So, how recycling works here?
    
    Let us break this down in steps.
    
    **Step 01.**
    
    First **item x** to **item 4** must be shown to screen at the initial launch. So, they are the five items that are in the visible view mode. Let's call them a **visible view.**
    
    And, **item 5** is the new item to be loaded when the list is scrolled up.
    
    **Step 02.**
    
    When we scroll one item above, **item x** moves up and a new item, **item 5** comes in the visible view category.
    
    Now, **item 6** is in the waiting view.
    
    Here **item x** has moved out from the visible view on top of the screen. This is called a **scrapped view.**
    
    > ScrapView is the view in RecyclerView which was once visible and now are not visible on the phone's screen to the user.
    > 
    
    # **Step 03.**
    
    Now, let's say we scrolled one more step up. This will move the **item 1** out of the screen and the **item 6** will move in.
    
    Here, **item 1** also becomes a scrapped view. Now, we have two scrapped views **item x** and **item 1**.
    
    They will be now stored in a collection of **scrapped views.**
    
    So, now when we have to load a new view in the visible view group, let's consider **item 7**, then the view from the collection from the scrapped view is used.
    
    # **Step 04.**
    
    Now, when we are loading **item 7**, we take a view from the collection of scrapped views. The view which we loaded from the scrapped view is called a **dirty view**.
    
    Now, the dirty view gets recycled and is relocated to the new item in the queue which has to be displayed on the screen i.e **item 7**.
    
    > The views which we take from scrap view collection and then after re-bound happens by the recyclerView adapter before it is drawn to the screen are called dirty views.
    > 
    
    ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/pages-for-view-recycler-7a25475edce4b0d5.jpg](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/pages-for-view-recycler-7a25475edce4b0d5.jpg)
    
    This is how recycling of views happens in recyclerView which is one of the main reasons for the better improvement of recyclerView. In this process, the views of the item are reused to draw new items on the screen.
    
    # **Usage of ViewHolder**
    
    The other way the views are optimized is because of ViewHolders in RecyclerView.
    
    So, let us say we have 100 items be displayed on the list and we want to show 5 items on the screen.
    
    Each item here has 1 TextView and 1 ImageView in the item.
    
    So, to map each view using findViewById is always an expensive task and just imagine the number of findViewByIds we might need to map all the TextViews and ImageViews of 100 items i.e 200 findViewByIds.
    
    So, when we are using RecyclerView, then only 6 items are created initially with 5 loaded at once to be displayed on-screen and one is the one to be loaded.
    
    Now, if we scroll the list then we have 7 viewHolders. One each for scrapped view and to be loaded view and 5 for the ones which are displayed.
    
    So, at a time, maximum findViewByIds that we are using are only 14 as we have a maximum of 7 ViewHolders.
    
- @JVM static, @JVM Overloads, @JVM Fields.
    
    @JVM static:-
    
    - This annotation is used to tell the compiler that the method is a static method and can be used in Java code.
    - Suppose we had a kotlin class and inside it we had some function, if we had to call these function inside another classt then we can call them by Calling the name of the class.function name ( e.g ClassName.functionName) but if we had to access the function inside the Java Class then either we had to call it using (e.g ClassName.Instance.FunctionName) or writing @JVM static annotation above the function.
    
    @JVM Overloads:- 
    
    - This annotation is used to tell the compiler that the method is a static method and can be used in Java code.
    - Suppose we had a function and it contains 2 parameter and both parameters are already defined then in kotlin calling that function seperately and assigning only 1 parameter value will work fine but in java it will ask for multiple parameter but if we had to assign only one parameter then we can usr @JVM Overloads const annotation on the function
    
    ( e.g @data class Event @JvmOverloads cons(val nam:String, val Date:Date = Date())
    
    @JVM Fields :-
    
    - To access the fields of a Kotlin class from Java code without using any getters and setters, we need to use the `@JvmField` in the Kotlin code.
    - If we had to access the parameter of any class then in kotlin we can do that with functionvarible.parameter but if we had to access it we had to use getter methord. If we don't want to use getter method then we had to annotate it with @JVM Field before assigning the varibale.
    
     ( e.g @data class Event @JvmOverloads cons(val nam:String, @Jvm Field val Date:Date = Date())
    
    Date data = event.date;
    
- **What do you mean by destructuring in Kotlin**
    - Destructing is a convient way of extracting multiple values from data stored in objects and arrays. or **destructuring declaration** is the one that creates and initializes multiple variables at once.
    - Thesre works on the component() functions. The number of variables that a destructing declaration can define, the class provide those number of component functions, starting from component1(), component2(), upto componentN(). Data class in kotlin by default implement Component functions.
    
    ```kotlin
    
    /**Destructuring declaration compiled to following code:-*/
    val emp_id = employee.component1()
    val salary = employee.component2()
    
    data class Data(val name: String, val age: Int)
    
    fun sendData(): Data {
        return Data("Aditya", 19)
    }
    
    fun main() {
    
    /** Using instance to access properties */
    val obj =sendData()
    println("Name is ${obj.name}")
    println("Age is ${obj.age}")
    
    /** Creating two variables using destructing declaration */
    val(name,age) =sendData()
    println("Name is $name")
    println("Age is $age")
    
    }
    ```
    
- Difference between == and ===
    - == is used to compare the value stored in the varibles are equal or not.
    - === is used to check if the reference of the variable are equal or not.
- What are Companion Objects in Kotlin
    - If you want to write a function or any member of the class that can be called without creating an instance of the class then you can write the same as a member of a companion object inside the class.
- init blocks
    
    Init block are the initializer blocks that are executed after the primary contructor is called. A class can have multiple init blocks and they all execute in a series. If you want to perform certain task then it will not be done into primary constructor it will be done inside the init blocks.
    
- Scope Function
    
    There are two main difference between the scope functions: 
    
    1. The way to refer to the context object ( either 'this' or 'it')
    2. The return value ( either 'context object' or the 'lambda result')
    - What are Scope Functions?
        - Makes your code consice and readable.
    - Types of Scope Functions?
        1. With :- return: lambda result, Context object: this (  which doesn’t provide lamda result)
        2. Let :- ( used for the null safety calls )
        3. Run :- (used for both compilation and initiazing)
        4. Apply :- return: context Object, context Object : this ( used for the initiazling)
        5. Also:- return: context object, Context Object: it ( used to perform any extra operation for the function )
- Extension Function
    
    Ability to add more functionality to the existing classes by without inheriting them. This is achieved through a feature known as extensions. When a function is added to an existing class it is known as extension functions.
    
    for more details refer [this](https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/ExtensionsFunctions/ExtensionFunction.kt)
    
- Suspend Function
    
    Suspend function is a function that could be started, paused and resume. And the important point about Suspend funciton that you are only allowed to called a suspend function from a Corouine or any other suspend function.
    
- Delay Functions
    
    It is a function which delays coroutine for a given time without blocking a thread, and resumes it after a specified time. When we add the suspend keyword in the function, all the cooperations are automatically done for us. We don't have to use when or switch cases in order to switch from one fuction to another.
    
- Inline Functions
    
    Inline function instruct compiler to insert complete body of the function wherever that function got used in the code.
    
    - Advantage
        - **Function** call overhead doesn't occur.
        - It also saves the overhead of push/pop variables on the stack when the **function** is called.
        - It also saves the overhead of a return call from a **function**. Such optimizations are not possible for normal **function** calls.
    - Implementation
        
        The decompiled code is as below:
        
        ```kotlin
        public void doSomething() {
           System.out.print("doSomething start");
           doSomethingElse();
           System.out.print("doSomething end");
        }
        
        public void doSomethingElse() {
           System.out.print("doSomethingElse");
        }
        ```
        
        As we can see here, the doSomething() function is calling the doSomethingElse() function as usual.
        
        Now let's try to add the inline keyword as below in the doSomethingElse() function.
        
        ```kotlin
        fun doSomething() {
            print("doSomething start")
            doSomethingElse()
            print("doSomething end")
        }
        
        inline fun doSomethingElse() {
            print("doSomethingElse")
        }
        ```
        
        Again, let's see the decompiled code. The decompiled code is as below:
        
        ```java
        public void doSomething() {
           System.out.print("doSomething start");
           System.out.print("doSomethingElse");
           System.out.print("doSomething end");
        }
        ```
        
        Now, we can see that the code of doSomethingElse() function is copied inside the doSomething() function. And the doSomething() function is no more calling the doSomethingElse() function.
        
    - So when to make the function inlie and when not:
        - When the function code is very small, it's good idea to make the function inline.
        - When the function code is large and called from so many places, it's a bad idea to make the function inline, as the large code will be repeated again and again.
- High-Order Functions
    - Defination
        
        A high order function that takes function as a parameter or return a function.
        
        It's a function which can take to do two things 
        
        1. Can take functions as parameters
        2. Can return a function 
    - Implementations
        
        ```kotlin
        
        /**
         * This takes a function abc: () -> Unit
         * () represents that function takes no parameters.
         * Unit represents that the function does not return anything
         * So, the passMeFunction can take a function that takes zero parameters and does not return anything.
         */
        fun passMeFunction(abc: () -> Unit) {
            //can take function, do something here and execute the function
            abc()
        }
        
        /**function can return a function*/
        fun add(a: Int, b: Int): Int {
            return a + b
        }
        
        /**
         * (Int,Int) means that the function should take two parameters both as the int
         * Int means that the function should return value as an int
         *
         */
        fun returnMeAddFunction() : ((Int,Int) -> Int) {
            return ::add
        }
        
        val add = returnMeAddFunction()
        val result = add(2,3)
        println(result)
        println(add)
        
        ```
        
    - Inline Function
        
        [https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/InlineFunctions/CrossInline.kt](https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/InlineFunctions/CrossInline.kt)
        
    - NoInline Function
        
        [https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/InlineFunctions/NoInlineFunction.kt](https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/InlineFunctions/NoInlineFunction.kt)
        
    - CrossInline function
        
        [https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/InlineFunctions/InLineFunctions.kt](https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/InlineFunctions/CrossInline.kt)
        
- Lambdas in Kotlin
    - Defination
        - Lambdas Expressions are essentially anonymous functions that we can treat as values – we can, for example, pass them as arguments to functions, return them, or do any other thing we could do with a normal object.
    - Implementation
        
        Lambda Expressions look like below:
        
        ```kotlin
        val square : (Int) -> Int = { value -> value * value }
        ```
        
        ```kotlin
        val nine = square(3)
        ```
        
        Now, let's learn it by a simple example in Kotlin:
        
        ```kotlin
        val doNothing : (Int) -> Int = { value -> value }
        ```
        
        This is a lambda expression that does nothing. Here the
        
        **`{ value -> value }`** is a complete function in itself. It takes an **int** as a parameter and returns a value as an **`int`**.
        
        In **`(Int) -> Int`**
        
        **`(Int)`** represents input **`int`** as a parameter.
        
        **`Int`** represents return type as an **`int`**.
        
        So, the **`doNothing`** is a function in itself that takes a value as an **`int`** and returns the same value as an **`int`**.
        
        Now another example:
        
        ```kotlin
        val add : (Int, Int) -> Int = { a, b -> a + b }
        ```
        
        This is also a lambda expression that takes two **`int`** as the parameters, adds them, and returns as an **`int`**.
        
        **`{ a, b -> a + b }`** is a function in itself that takes two **`int`** as the parameters, adds them, and returns as an **int**.
        
        In **`(Int, Int) -> Int`**
        
        **`(Int, Int)`** represents two **`int`** as the input parameters.
        
        **`Int`** represents return type as an **`int`**.
        
        So, the **`add`** is a function in itself that takes two **`int`** as the parameters, adds them, and returns as an **`int`**.
        
        We can call it very similar as we do with the function like below:
        
        ```
        val result = add(2,3)
        ```
        
        Now, that we have understood the lambda expressions. Let's move to the Higher-order functions.
        
        ```java
        
        /**
         * { value -> value } is a complete function in itself.
            It takes an int as a parameter and returns a value as an int.
         * In (Int) -> Int
         * (Int) represents input int as a parameter.
         * Int represents return type as an int.
         */
        val square: (Int) -> Int ={value->value * value}
        val nine = square(3)
        println(nine)
        
        /**
         * Here do Nothing is the function in itself that takes the value as int and return same value as int
         */
        val doNothing : (Int) -> Int ={value->value}
        println(doNothing(3))
        
        /**
         * This is also a lambda expression that takes two int as the parameters, adds them, and returns as an int.
         * { a, b -> a + b } is a function in itself that takes two int as the parameters, adds them, and returns as an int.
         * In (Int, Int) -> Int
         * (Int, Int) represents two int as the input parameters.
         * Int represents return type as an int.
         * So, the add is a function in itself that takes two int as the parameters, adds them, and returns as an int.
         */
        val add : (Int, Int) -> Int ={a, b->a + b}
        println(add(10,20))
        
        ```
        
        Refer this for good explanation : [Link](https://github.com/chekeAditya/Data-Structure-Algorithm/blob/main/CodingTask/Lambdas_Expressions/Lambdas_Function.kt)
        
- Communication Between Suspend function
    
    ```kotlin
    
    // arbitrary do task function for explanation
    suspend fun dotask(request: Request): Response
    {
        // perform the task
    }
    
    /* Though it seems that only one argument has passed to dotask() function, but internally there are two arguments. Internally, it gets converted by the compiler to another function without the suspend keyword with an extra parameter of the type Continuation<T> like below:*/
    
    // internal conversion of suspend function dotask()
    fun dotask(request: Request, continuation: Continuation)...
    
    /*The way suspend functions communicate with each other is with Continuation objects. A Continuation is just a generic callback interface with some extra information, which looks like below(taken from Kotlin source code): */
    
    // Continuation interface structure
    public interface Continuation<in T>
    {
        public val context: CoroutineContext
        public fun resumeWith(result: Result<T>)
    }
    
    /* context:- will be the CoroutineContext to be used in that continuation.
    resumeWith:- resumes execution of the coroutine with a Result, that can contain either a value which is the result of the computation that caused the suspension or an exception.*/
    
    The two extension functions of resumeWith are given by:
    
    fun <T> Continuation<T>.resume(value: T)
    fun <T> Continuation<T>.resumeWithException(exception: Throwable)
    
    /*We can see the two extension function that they can be used to resume the coroutines with a return value or with an exception if an error had occurred while the function was suspended. This way, a function could be started, paused, and resume with the help of Continuation. We just have to use the suspend keyword.*/
    ```
    
- What is Enum Classes
    - An `enum` is a special "class" that represents a group of **constants** (unchangeable variables, like `final` variables).
    - An enum class is just like the class have attributes and methods. The only difference is that enum constants are public, static and final (unchangeable-cannot be overridden)
- Sealed Classes?
    - As the word sealed suggests, sealed classes conform to **restricted** or **bounded class hierarchies**. A sealed class defines a set of subclasses within it. It is used when it is known in advance that a type will conform to one of the subclass types. Sealed classes ensure type-safety by restricting the types to be matched at compile-time rather than at runtime.
    - Prevent people from extending any random classes or making any random class of a subclass of any other class. The answer to this particular class is sealed class.
- How viewModel Work Internally
    - Definations
    - Advantages of Viewmodel
        - Handle Configuration Changes → it automatically retained whenever activity is recreated due to configuration changes
        - Lifecycle Awareness → Viewmodel objects are also lifecycle-aware. They are automatically cleard when the lifecycle they are observing gets permantly destroyed.
        - Data Sharing → Data can be easily shared betweeen fragment in an activity using viewModels.
        - Kotlin-Coroutine Support → ViewModel include kotlin-coroutines so they can easity integrated for any asynchronous processing.
    - Internal working
        
        Refer thi s [link](https://blog.mindorks.com/android-viewmodels-under-the-hood) 
        
- Visibility Modifier's
    - Public:- This means that Declaration are visible everywhere.
    - internal:- declarations are visible inside a module.
        
        A *module* in kotlin is a set of Kotlin files compiled together. *modules* can be: maven projects, gradle sets, files generated from an Ant task, or a IntelliJ IDEA module
        
         *internal* provides real encapsulation for the implementation details, while in Java’s *package-private* encapsulation could be broken. External code can define classes in the package you are trying to protect.
        
    - private:-  With *private* declarations are only visible in the class as in Java but in Kotlin also in the file (top level declarations) where it is declared.
        
        Another difference is that in Kotlin *outer* classes do not see *private* *nested* (or *inner*) classes
        
    - Proceted:- Declarations are only visible in its class and in its subclassess
- Difference between open and public
    
    **public**: public keyword in Kotlin is similar to java it is use to make the visibility of classes, methods, variables to access from anywhere.
    
    **open**: In Kotlin all classes, functions, and variables are by defaults final, and by inheritance property, we cannot inherit the property of final classes, final functions, and data members. So we use the open keyword before the class or function or variable to make inheritable that.
    
- What is dispatchers and there types in Coroutines
    - Dispacthers helps coroutines in deciding the thread on which the work has to be done. Dispatchers are passed as an arguments in the GlobalScope by mentioning which type of dispatchers we can use depending on the work that we want the coroutine to do.
    - Types of Dispatchers
        - Main Dispatcher:-
            
            It starts the coroutine in the main thread. It is mostly used when we need to perform the UI operations within the coroutine, as UI can only be changed from the main thread(also called the UI thread).
            
        - IO Dispatcher:-
            
            It is used to perform all the data operations such as networking, reading, or writing from the database, reading, or writing to the files eg: Fetching data from the database is an IO operation, which is done on the IO thread.
            
        - Default Dispatcher:-
            
            We should choose this when we are planning to do Complex and long-running calculations, which can block the main thread and freeze the UI eg: Suppose we need to do the 10,000 calculations and we are doing all these calculations on the UI thread ie main thread, and if we wait for the result or 10,000 calculations, till that time our main thread would be blocked, and our UI will be frozen, leading to poor user experience. So in this case we need to use the Default Thread. The default dispatcher that is used when coroutines are launched in GlobalScope is represented by Dispatchers. Default and uses a shared background pool of threads, so launch(Dispatchers.Default) { … } uses the same dispatcher as GlobalScope.launch { … }.
            
        - UnConfined Dispatcher:-
            
            As the name suggests unconfined dispatcher is not confined to any specific thread. It executes the initial continuation of a coroutine in the current call-frame and lets the coroutine resume in whatever thread that is used by the corresponding suspending function, without mandating any specific threading policy.
            
- Coroutines
    
    ***coroutines are lightweight threads. By lightweight,** **it means that creating coroutines doesn’t allocate new threads. Instead, they use predefined thread pools and smart scheduling for the purpose of which task to execute next and which tasks later**.*
    
- Coroutines vs Threads?
    - Fetching the data from one thread and passing it to another thread takes a lot of time. It also introduces lots of callbacks, leading to less readability of code. On the other hand, coroutines eliminate callbacks.
    - Creating and stopping a thread is an expensive job, as it involves creating their own stacks.,whereas creating coroutines is very cheap when compared to the performance it offers. coroutines do not have their own stack.
    - Threads are blocking, whereas coroutines are suspendable. By blocking it means that when a thread sleeps for some duration, the entire threads get blocked, it cannot do any other operation, whereas since coroutines are suspendable, so when they are delayed for some seconds, they can perform any other work.
    - Coroutines offer a very high level of concurrency as compared to threads, as multiple threads involve blocking and context switching. Context switching with threads is slower as compared to coroutines, as with threads context can only be switched when the job of 1 thread gets over, but with coroutines, they can change context any time, as they are suspendable.
    - Coroutines are light and super fast. Coroutines are faster than threads, as threads are managed by Operating System, whereas coroutines are managed by users. Having thousands of coroutines working together are much better than having tens of threads working together.
- SupervisorJob(), Coroutine Exception Hangling
    
    ```kotlin
    fun main(): Unit =runBlocking{
    
    val exceptionHandler =CoroutineExceptionHandler{coroutineContext, throwable->
    
    println("debug: exception handler caught some error ${throwable.message}")
    }
    
    /*If any one coroutine throws an error and you don't want it should thrown an error then use SupervisorJob() */
        val parent =CoroutineScope(IO+ exceptionHandler +SupervisorJob())
    
        val child1 = parent.launch{
    println("debug:coroutine 1 started")
            delay(100)
            throw RuntimeException()
    }
    
    child1.invokeOnCompletion{
    if (itis CancellationException) {
    println("child1 cancelled")
            }
    }
    
    val child2 = parent.launch{
    println("debug:coroutine 2 started")
            delay(100)
            throw RuntimeException()
    }
    
    child2.invokeOnCompletion{
    if (itis CancellationException) {
    println("child2 cancelled")
            }
    }
    }
    ```
    
- Scope in Kotlin Corountine?
    - Global Scope
        
        → Global scope live long till the application does. It's coroutines finish it's work it will be destroyed it and will not keep alive unitl the application dies.
        
        - But what if coroutine work is still pending and we closed the applciation?
            
            → in this scenario the coroutine will also dies as lifecycle of coroutine is equal to the lifetime of the application. Coroutines launched in the global scope will launched in the seperate thread.
            
        
        → Using global scope is not always good as it stay alive untill activity stays alive.
        
    - Lifecycle Scope
        - It's same like global Scope but the difference is that when we use the lifecycle scope, all the coroutines launched within the activity also dies when the activity dies.
        - it's necessary as our corutines will not keep running even after our activity dies.
        - Implementation :- instead of Global scope write lifecycle scope.
    - ViewModel Scope
        
        It is also the same as the lifecycle scope, only difference is that the coroutine in this scope will live as long the viewmodel is alive. ViewModel is a class that manages and stores the UI-related data by following the principles of the **[lifecycle system in android.](https://www.geeksforgeeks.org/activity-lifecycle-in-android-with-demo-app/)**
        
- Async{ } and launch{ }
    - launch() → `launch{}` does not return anything, it's like fire and forget
    - async() → `async{}`returns an instance of `Deferred<T>`, which has an `await()`function that returns the result of the coroutine like we have future in Java in which we do future.get() to the get the result. and it perform a task and return a result
    
    ```kotlin
    //async
    fun main(): Unit =runBlocking{
    
    val res1: Deferred<Int> =async{
    return@async num1()
    }
    
    val res2: Deferred<Int> =async{
    return@async num2()
    }
    
    print("The result is ${res1.await() + res2.await()}") //  o/p will 3
    }
    
    private suspend fun num1(): Int {
        delay(300)
        return 1
    }
    
    private suspend fun num2(): Int {
        delay(300)
        return 2
    }
    ```
    
- **Livedata**
    - LiveData is an observable data holder class that is used to observe the changes of a ViewModel and update those changes.
    - LiveData is lifecycle-aware, which means that whenever data is updated or changed, the changes are only applied to the specific app components that are in an active state. Contrarily, if the app components are inactive, the changes will not be applied
    - **Synchronous vs Asynchronous Update**
    
    LiveData doesn’t have public methods to update its value. Hence you’ll use `MutableLiveData` to update the value inside LiveData with the help of the following two options:
    
    1. `setValue`: sets the value instantly. This is synchronous update where main thread calls `setValue`. With Kotlin’s property access syntax, you’ll often use `value` instead of `setValue`.
    2. `postValue`: Asynchronous updating, means Observer doesn’t receive instant update, rather receives update when UI thread is active. When you call `postValue` more than one time from background thread, LiveData dispatches only the latest value to the downstream. Being asynchronous, this does not guarantee instant update to the Observer.
    - **Why do we need LiveData?**
        - It removes the leaks caused by the interfaces/callbacks that send results to the UI thread. This is a core feature of an MVVM model where callbacks are sent from ViewModel to activity/fragment.
        - It de-couples tight integration between data, mediator, and the UI layers.
    - **Using LiveData**
        
        In order to use LiveData in your Android project, follow these steps:
        
        1. Create a LiveData instance in your ViewModel class to hold the data.
        2. Set the data in LiveData using setValue().
        3. Return the LiveData using postValue(). Only this data will be observable by the Observer which is in Views i.e., activity or fragment.
        4. Finally, observe the data with the help of the Observer() function. Inside Observer(), you can define all your necessary changes in the UI that you want to perform when there is a change or update in the data.
    - **Advantages of using LiveData**
        - **Ui matches with the data state.**
            
            LiveData follows the Observer pattern. In an active state, whenever a component’s data gets changed or updated, the particular component UI matches the state without fail. We don't need to update the UI every time the app data changes because the Observer takes care of that.
            
        - **Increased stability of code**
            - There are no crashes when activities are stopped. If the app components are inactive those changes are not affected. So, you need not worry about the app component lifecycle while updating the data. And in the case of an activity in the back stack, it doesn’t receive any LiveData events.
            - Memory leaks will be reduced because unwanted events/allocations are automatically handled
            - No concerns while unsubscribing any Observers
            - Changes need not be updated in the latest data during a configuration/screen orientation change
        - **No manually lifecycle Handling.**
            
            LiveData is aware of the View's lifecycle. Therefore, the UI components just observe relevant data and don’t stop or resume observation. LiveData automatically manages all of these changes while observing
            
        - **Always up to date with the latest data**
            
            Whenever there is a change in the data stored in LiveData, all the observers associated with the LiveData will be notified (only when the app components are live). If any app component is in an inactive state, LiveData concept will not work. But the latest data will be observed by the Observer. When the component is reactivated, the most recent data will be applied to it.
            
        - **Proper configuration changes/screen orientation**
            
            If an activity or fragment is recreated due to a configuration change or screen orientation, it immediately receives the latest available data and updates the UI.
            
        - **Sharing resources**
            
            Like the Singleton pattern, we can extend our LiveData object too to wrap system services so that they can be shared in our app. Once the LiveData object connects to the system service, any observer that needs the resource can watch the LiveData object easily.
            
    - Just a **Deep Dive(optional)**
        
        
- Types of LiveData
    - LiveData
        
        is immutable by default. By using LiveData we can only observe the data and cannot set the data.
        
    - MutableLiveData
        
        mutable and is a subclass of LiveData. In MutableLiveData we can observe and set the values using postValue() and setValue() methods (the former being thread-safe) so that we can dispatch values to any live or active observers.
        
    - MediatorLiveData
        
        can observe other LiveData objects such as sources and react to their onChange() events. MediatorLiveData will give us control over when we want to perform an action in particular or when we want to propagate an event.
        
    - SingleLiveEvent
        
        LiveData will trigger upon configuration change or screen rotation. But in some scenarios, like when we need to perform UI updates by clicking on a particular View to perform validations or show a progress bar during server call, we go with SingleLiveEvent.
        
        ***SingleLiveEvent*** is a subclass of MutableLiveData. It is aware of the View's lifecycle and can observe the data with a single Observer.
        
- Work Manager?
    - Depth
        
        Work manager is part of Android Jetpack Libraries and an architecture Component mainly intended for doing long-running background tasks.
        
        Basics of WorkManager
        
        - Constaints
            
            Contraints → before starting the work we may have some predefined constraints. like task may need network connectivity if it’s related to network, or it can be battery efficient. It can be single or multiple constraints based on the requirement.
            
            ```kotlin
            val constraints = Constraints.Builder()
                .setRequiredNetworkType(NetworkType.CONNECTED)
                .setRequiresBatteryNotLow(true)
                .setRequiresStorageNotLow(true)
                .setRequiresCharging(true)
                .setRequiresDeviceIdle(true)
                .build()
            ```
            
        - Worker
            - Task or work that need to be performed is defined using worker class.
            - It’s an abstract class so we need to subclass it and override the method `doWork()` ****where we do our actual work implementation.
            - `Worker` class is responsible for performing work synchronously on a background thread provided by `WorkManager`
                
                ```kotlin
                class UploadLogsWorker(appContext: Context, workerParams: WorkerParameters)
                    : Worker(appContext, workerParams) {
                
                    override fun doWork(): Result {
                        try {
                            val response = uploadLogData()
                        } catch (e: Exception) {
                            e.printStackTrace()
                            return Result.failure()
                        }
                
                        // Indicate whether the task done successfully
                        return if(response.isSuccess) Result.success() else  Result.retry()
                    }
                
                    fun uploadLogData(imageUri: String): Response {
                        // API service request code goes here
                    }
                }
                ```
                
            - `Result.success()` : Returns an instance of Result that can be used to indicate that the work is completed successfully
            - `Result.failure()` : Returns an instance of Result that can be used to indicate that the work is completed with a permanent failure
            - `Result.retry()` : Returns an instance of Result that can be used to indicate that the work is encountered a transient failure and should be retried with backoff policy
        - WorkRequest
            
            Defines how and when the work should be executed. Each work must have a work request for scheduling.
            
            - `OneTimeWorkRequest`**:** Basically used for a one-time execution of a task. For non-repeating tasks
            
            ```kotlin
            val uploadWorker = OneTimeWorkRequestBuilder<UploadLogsWorker>()
                .setConstraints(constraints)
                .build()
            ```
            
            - `PeriodicWorkRequest`**:** Where a task needs to be executed on a recurring basis. For repeating tasks
            
            ```kotlin
            
            // Create periodic worker with 10 hours interval
            val uploadWorker = PeriodicWorkRequest.Builder(
                UploadLogsWorker::class.java, 10, TimeUnit.HOURS)
                .setConstraints(constraints)
                .build()
            ```
            
        - WorkManger
            
            Once the work request is defined now we can schedule it with WorkManager. We call `enqueue()` ****to schedule a request
            
            ```kotlin
            WorkManager.getInstance(this).enqueue(uploadWorker)
            ```
            
        - WorkStatus
            - Once the work is enqueued the only thing we need to know is the status of the work and the output.
            - For all the work requests scheduled, WorkManager maintains a LiveData which we can get by using the tag or request-id. Tag is the string that we provide while enqueuing requests with the WorkManger.
            
            ```kotlin
            //Getting work status By using request ID
            val workInfo = WorkManager.getInstance(this).getWorkInfoByIdLiveData(uploadWorker.id)
            
            //Getting work status By using Tag
            val workInfo = WorkManager.getInstance(this).getWorkInfosByTag("tag_pasted")
            
            ```
            
        - Cancelling
            - If we want to cancel any scheduled work WorkManger provides us the flexibility to do that either by using the id of the work request or by the tag.
            
            ```kotlin
            val workManager = WorkManager.getInstance(this)
            //Cancels work with the given id if it isn't finished.
            workManager.cancelWorkById(id)
            
            // Cancels all unfinished work with the given tag.
            workManager.cancelAllWorkByTag("tag")
            
            //Cancels all unfinished work. By invoking cancelAllWork(),
            // we will potentially affect other modules or libraries in our project.
            workManager.cancelAllWork()
            ```
            
        - Delayed Work
            
            We can delay the initial work execution using `setInitialDelay()`:
            
            ```kotlin
            val myWorkRequest = OneTimeWorkRequestBuilder<MyWork>()
                .setInitialDelay(5, TimeUnit.MINUTES)
                .build()
            ```
            
        - Retry and Backoff Policy
            
            When a worker returns `Result.retry()` then `WorkManger` will reschedule the work based on backoff criteria. The backoff criteria are defined by two properties
            
            - `BackoffDelay` ****specifies the minimum amount to wait before retrying the work. Defaults to 10 seconds
            - `BackoffPolicy` defines how the backoff delay should increase over time for subsequent retry attempts. WorkManager supports 2 backoff policies, `[LINEAR](https://developer.android.com/reference/androidx/work/BackoffPolicy#LINEAR)` and `[EXPONENTIAL](https://developer.android.com/reference/androidx/work/BackoffPolicy#EXPONENTIAL)`. Backoff policy by default is exponential, but can be set to linear.
            
            ```kotlin
            val uploadWorkeRequest = OneTimeWorkRequestBuilder<UploadLogsWorker>()
                .setBackoffCriteria(
                    BackoffPolicy.LINEAR,
                    MIN_BACKOFF_MILLIS,
                    TimeUnit.MILLISECONDS)
                .build()
            ```
            
        - Chaining
            - We can easily chain multiple requests through WorkManager.
            - Let's suppose we have three requests to be executed at the start parallelly and the next requests should be executed once the first three requests are successfully completed then we can specify them as below using `begin` and `then`
            
            ```kotlin
            WorkManager.getInstance(this)
            .beginWith(Arrays.asList(workRequest1,workRequest2, workRequest3))
            .then(workRequest4)
            .then(workRequest5)
            .enqueue()
            ```
            
            - *Note: The begin and then methods take `OneTimeWorkRequests` ****and ****if any work in the chain fails or is cancelled, all of its dependent work inherits that state and will never run.*
        - How is work guranteed with work manager?
            - When we enqueue a work with WorkManger an internal TaskExecutor saves our `WorkRequest` info to the WorkManager database.
            - After the request is saved whenever the constraints are met the Internal TaskExecutor uses `WorkerFactory` to create a `Worker` .
            - We can customize the worker factory. Once the worker is created it gets executed in an executor
            
            ![https://miro.medium.com/max/541/1*-r6dTUdIN3FG_h2RpN8YLw.png](https://miro.medium.com/max/541/1*-r6dTUdIN3FG_h2RpN8YLw.png)
            
            ![https://miro.medium.com/max/875/1*4yL7HDWB8xQtjdrOaTPLnQ.png](https://miro.medium.com/max/875/1*4yL7HDWB8xQtjdrOaTPLnQ.png)
            
        - LifeCycler of One Time Request
            - As we can see the initial state will be either blocked or mostly enqueued depending on the state of WorkManager.
            - It enters into a running state once the execution of workers is started. From running state it mostly should result in either success or failure. But there might be cases where we want to retry or cancel the ongoing request based on the requirement.
            
            ![https://miro.medium.com/max/875/1*nzZ-7H_q2v8w1vI1DQJ47Q.png](https://miro.medium.com/max/875/1*nzZ-7H_q2v8w1vI1DQJ47Q.png)
            
        - Lifecycle of periodic requests
            - In most cases, it’s similar to a one-time request but the only change is even if the request is successfully executed it will be enqueued again based on the interval we have provided.
            
            ![https://miro.medium.com/max/875/1*TP5H7PX4q1XtKqF_4Wh09Q.png](https://miro.medium.com/max/875/1*TP5H7PX4q1XtKqF_4Wh09Q.png)
            
    
    ---
    
    Work Manager is a library part of Android Jetpack which makes it easy to schedule deferrable, asynchronous tasks that are expected to run even if the app exits or device restarts i.e. even your app restarts due to any issue Work Manager makes sure the scheduled task executes again.
    
    - Integration
        
        To Integrate work manager in your project,
        
        ```kotlin
        dependencies {
          def work_version = "2.2.0"
            implementation "androidx.work:work-runtime:$work_version"
          }
        ```
        
        Now, as a next step, we will create a **Worker** class. Worker class is responsible to perform work synchronously on a background thread provided by the work manager.
        
        ```kotlin
        classYourWorkerClass(appContext:Context,workerParams:WorkerParameters):Worker(appContext,workerParams) {
        
            override fundoWork(): Result {
        // Your work here.// Your task resultreturn Result.success()
            }
        }
        ```
        
        - doWork() method is responsible to execute your task on the background thread.
        - Result returns the status of the work done in doWork() method. If it returns Result.success() it means the task was successful if the status is Result.failure(), the task was not-successful and lastly, if it returns Result.retry() it means the task will execute again after some time.
        
        We need to create a WorkRequest which defines how and when work should be run. It has two types,
        
        - OneTimeWorkRequest - Runs the task only once
        - PeriodicWorkTimeRequest - Runs the task after a certain time interval.
        
        ```
        val yourWorkRequest = OneTimeWorkRequestBuilder<YourWorkerClass>().build()
        ```
        
        and once we have defined our work request, we can just schedule the task using,
        
        ```
        WorkManager.getInstance(context).enqueue(yourWorkRequest)
        ```
        
- What is the difference between member variable and variable created inside a method?
    
    Local variable:- 
    
    - created and declareid in method, constructors, blocks and once the method, constructor or block get destroyed it exits the method
    - cannot use access modifiers
    - There is no default value for local variables, so local variables should be declared and an initial value should be assigned before the first use.
    
    Member/Instance Variable
    
    - declared in a class but outside the method, constructor or blocks
    - hold values that must be referenced by more than one method, construtor or block state that must be present throghout the class.
    - access modifieers can be declared for instance variables.
    - these are visible for all the methods, constructor,class.
    - it's has it's default value i..e 0, booleadn it is false and for object it is null.
    - Instance variables are created when an object is created with the use of the keyword 'new' and destroyed when the object is destroyed.
- what is the default value of the Sting member variable and member object ?
    - Integers
        
        Variables of type "int" have a default value of 0.
        
    - Numbers
        
        Variables of type "Number" have a default value of NaN. NaN means Not a Number.
        
    - Booleans
        
        Variables of type "Boolean" have a default value of false.
        
    - Strings
        
        Variables of type "String" are treated as Objects in this case and have a default value of null.
        
    - Objects
        
        Variables of any "Object" type (which includes all the classes you will write) have a default value of null.
        
        *All member variables of a Newed object should be assigned a value by the objects constructor function. If not, then the above rules apply!*
        
- In how many ways can you create object of String ?
    1. String literal.
        1. String s="welcome";
        
        → Each time you create a string literal, the JVM checks the "string constant pool" first. If the string already exists in the pool, a reference to the pooled instance is returned. If the string doesn't exist in the pool, a new string instance is created and placed in the pool. For example:
        
    2. By new Keyword.
        1. String s=**new** String("Welcome");//creates two objects and one reference variable
        
        → In such case, [JVM](https://www.javatpoint.com/jvm-java-virtual-machine) will create a new string object in normal (non-pool) heap memory, and the literal "Welcome" will be placed in the string constant pool. The variable s will refer to the object in a heap (non-pool).
        
- Why java uses the concept called String literal?
    
    TO make java more memory eficient.(because no new objects are created if it exists already in the string constat pool)
    
- What is String?
    
    String is a sequence of characters. But in Java, string is an object that represents a sequence of characters. The java.lang.String class is used to create a string object.
    
- String pool?
    
    Caching the string literals and reusing them saves a lot of heap space because different String variables refer to the same object in the string pool. String intern pool serves excatly this purpose.
    
    Java String Pool is **the special memory region where *Strings* are stored by the JVM**. Since *Strings* are immutable in Java, the JVM optimizes the amount of memory allocated for them by storing only one copy of each literal *String* in the pool. This process is called interning:
    
    ```
    String s1 = "Hello World";
    String s2 = "Hello World";
    
    assertThat(s1 == s2).isTrue();
    ```
    
- Why String class is Final in Java?
    
    The reason is because no one can override the methods of the string clas. So that it can provide the same features to the new objects as well as to the old ones.
    
- Why String objects are immutable in Java?
    
    The krey benefits of kepping the string immuable are caching, security, synchronizaration and performance.
    
    - If you want to increse the performace of the Sting make immuatable.
    - Memory Optimization:- String objects are cached in String pool. as duplicate are not allowed in the String contraint pool
- StringBuffer?
    
    It's a class used to create mutable(modifiable) String objects. The StringBuffer class in java is the same as String class except it is mutable i.t it can be changed.
    
- Static Keyword in java?
    - Used for memory management, used to share same varible or method of a given class. Belong to the class then instance of the class.used for constant variable or method that is sane for every instance of the class.
    - When a member is declared as static it can be accessed before any objects of it's classes and withour referecce to any object.
    - you can declare a static block that gets executed exactly once, when the class is first loaded.
    - We can create static variables at the class level only. See **[here](https://www.geeksforgeeks.org/g-fact-47/)**
    - static block and static variables are executed in the order they are present in a program.
- Why main is static ?
    - Main method is always static so that compiler can call it without creation of an object or before the creation of the object.
    - In any Java program, the **main()** method is the starting point from where compiler starts program execution. So, the compiler needs to call the main() method.
    - If the **main()** is allowed to be non-static, then while calling the **main()** method JVM has to instantiate its class.
- Understanding public static void main (String[] args) in java?
    1. Public :- It is the access modifier, which specifies from where and who can access the method. Making main() method public makes it globally [available. It](http://available.It) is  made public so that JVM can invoke it from outside the class as it's not present in current class.
    2. Static:- It is a *keyword* which is when associated with a method, makes it a class related method. The *main()* method is static so that JVM can invoke it without instantiating the class. This also saves the unnecessary wastage of memory which would have been used by the object declared only for calling the *main()* method by the JVM.
    3. void :- It is a keyword and used to specify that a method doesn’t return anything. As *main()* method doesn’t return anything, its return type is *void*. As soon as the *main()* method terminates, the java program terminates too. Hence, it doesn’t make any sense to return from *main()* method as JVM can’t do anything with the return value of it.
    4. main:- It is the name of Java main method. It is the identifier that the JVM looks for as the starting point of the java program. It’s not a keyword.
    5. String[] args:- It stores Java *command line arguments* and is an array of type *java.lang.String* class. Here, the name of the String array is *args* but it is not fixed and user can use any name in place of it.****
- which executes first ? static blocks or main()
    
    static block is executed before the main method at the time of class loading.
    
- Can we have a try block without catch or finally block ?
    
    Yes it's possible to have a try block without catch block. But we don't have catch block only try then it will not work with error 
    java: 'try' without 'catch', 'finally' or resource declarations
    
- Can a finally block exist without try?
    
    No 
    
- why static variables/functions are called class variables/functions?
    
    Class variable are also known as static variables as static varibales are declared with the static keyword in a class but outside a method or constructor or a block.
    
- Can we have duplicate keys in hashmap?
    
    No we cannot add duplicate keys into the hashmap, but we add the key which already present inside the hashmap then it till replace it's value with the new value.
    
- How does hashmap work internally ? (research)
- Can we have duplicate values in hashmaps?
    
    Yes we can have duplicate value in the hashmap but the should be unique.
    
- What is inheritance and give a practical example?
    
    Inhertance is something where you had to inherite some feature from you parent or in java when a class inherits some method from it's parent class then it's called as Inheritance
    
    ```kotlin
    
    public class Commercial { //parent class
    
        String nameOfCustomer;
    
        public String getNameOfCustomer() {
            return nameOfCustomer;
        }
    
        public void setNameOfCustomer(String nameOfCustomer) {
            this.nameOfCustomer = nameOfCustomer;
        }
    
        public void CalculateBills(int unit) {
            int bill_amt = 5 * 100;
            System.out.println("Bill amount = " + bill_amt + " Rs");
        }
    }
    ```
    
    ```kotlin
    public class Domestic extends Commercial { //child class
    
        @Override
        public String getNameOfCustomer() {
            return super.getNameOfCustomer();
        }
    
        @Override
        public void setNameOfCustomer(String nameOfCustomer) {
            super.setNameOfCustomer(nameOfCustomer);
        }
    
        @Override
        public void CalculateBills(int unit) {
            int bill_amt_domestic = (int) (2.5 * 100);
            System.out.println("Bill amount = " + bill_amt_domestic + " Rs");
        }
    }
    
    //Driver class
    package Basic_To_Advanced_DataStructure.CodingTask.InheritanceAndEncapsulation.CalculatingBills;
    
    public class Drive {
        public static void main(String[] args) {
            Commercial commercial = new Commercial();
            commercial.setNameOfCustomer("Raj Kumar");
            System.out.println("Customer: " + commercial.nameOfCustomer);
            commercial.CalculateBills(100);
    
            System.out.println();
            Domestic domestic = new Domestic();
            domestic.setNameOfCustomer("Lalith Raj");
            System.out.println("Customer: " + domestic.nameOfCustomer);
            domestic.CalculateBills(100);
        }
    }
    ```
    
- What is a final variable ?
    - Final keywod is the non-access specfier that is used to restrict a class, variable, method. If we initialize a variable with the final keyword then we cannot modify it later.
    - Final variable → used to create constants.
    - Final Classes → used to prevennt inheritance
    - Final Methods → used to prevent method overriding.
- What happens when a class is final ?
    
    to prevent the class from being subclassed. If a class is marked as final then no class can **inherit** any feature from the **final class.**
    
- What happens if a method is made final ?
    
    Whenever you make a method final, you cannot **override** it. i.e. you cannot provide implementation to the superclass’s final method from the subclass.
    
    i.e. The purpose of making a method final is to prevent modification of a method from outside (child class).
    
- Which constructor is called first when child class object is created ? Parent or child
    
    Parent construtor 
    
    ---
    
    Whenever a subclass's constructor is called , the first default statement in it is super(); which is automatically added by the compiler,The super(); will invoke the constructor of superclass and so, first it will execute MainConstructor() and then ChildConstractor() Refer to this : [https://www.javatpoint.com/super-keyword](https://www.javatpoint.com/super-keyword)
    
    Even if you want to specify super(); it needs to be the first statement of your constructor else it will give you compile time error!
    
    Your Constructor is like this :
    
    ```
    public ConstractorDemo()
    {
       super(); // u didn't specified this but compiler will automatically add it
       System.out.print("Demo");
    }
    ```
    
- What is super() keyword in java?
    
    A super keyword in java is a reference variable which is used to refer immediate parent class object. Whenever you create the instance of subclass, an instance of parent class is created implicitly which is refered by super reference varibale.
    
    ---
    
    ---
    
    usage of java Super Keyword
    
    - used to refer the immediate parent class method.
    - used to invoke immediate parent class instance variable
    - used to invoke immediate parent class constructor
- What is the difference between static and non static variables ?
    - static blocks can override in non static methods
    - non static cant overide in static methods
- Answer for stack over flow exception
    
    The exception that is thrown when the execution stack overflows because it contains too many nested method calls. This class cannot be inherited.
    
    `StackOverflowException` is thrown for execution stack overflow errors, typically in case of a very deep or unbounded recursion. So make sure your code doesn't have an infinite loop or infinite recursion.
    
- What are .dex files?
    
    dex file is a file that is executed on the Dalvik VM.
    Dalvik VM includes several features for performance optimization, verification, and monitoring, one of which is Dalvik Executable (DEX).
    Java source code is compiled by the Java compiler into .class files. Then the dx (dexer) tool, part of the Android SDK processes the .class files into a file format called DEX that contains Dalvik byte code. The dx tool eliminates all the redundant information that is present in the classes. In DEX all the classes of the application are packed into one file. 
    
- What is DDMS?
    
    The Dalvik Debug Monitor Service (DDMS) is a debugging tool used in the Android platform. The Dalvik Debug Monitor Service is downloaded as part of the Android SDK. Some of the services provided by the DDMS are port forwarding, on-device screen capture, on-device thread and heap monitoring, and radio state information.**The main services provided by Dalvik Debug Monitor Server are:**
    
    - App memory usage statistics (total heap and object allocation statistics)
    - App thread statistics
    - Device screen capture
    - Device file explorer
    - Incoming call and SMS spoofing
    - Location data spoofing
    - Logcat
- Explain Android System architecture.
    
    ![https://elinux.org/images/c/c2/Android-system-architecture.jpg](https://elinux.org/images/c/c2/Android-system-architecture.jpg)
    
    - Having Basically the 5 layer architecture
    1. Linux kernel →  The main work on kernel is to get the work done by hardware like display drivers, camera drivers, flash memory driver etc.
    2. Libraries → it's nothing but some logical group of instructions that we want to give to the kernel to perform an action is been done by libraries. like sqLite libraries, SGL Libraries and etc
    3. Applciation Framework → These are basically group of instances put together for the purpose of the developer to make things easy and understandable. like we have activity manager or telephoy manager role would be get call, make call
    4. Applciations → Application which are available in the andoid phone itself are known as application like Home, Contacts, Phone, Browser etc.
        
        → Application which are developed my us are known as user developed applications.
        
        → Basically application contains all the UI like facebook , instagram home etc
        
    5. Android RunTime → 
        - As we know the java has the JVM i.e Java Virtual Machine same way in android we had DVM :- Dalvik Virtual machine.
        - in java we had .jar files but in andorid we had .dex files → these dex files are very better for our development wise as they are compact and efficient then class files.
        - Why Compact ? → as they are using less memories as they are using the limited memory then battery power will be also be low and battery will be improve
        - We also had core libraries like java edition, collection ,I/O these all colect together to form an Android Runtime.
    
    ---
    
    Linux Kernel : Divide in   to three main parts 
    
    ---
    
    1. Device Driver → Getting work done by kernel 
    2. Memory Management → it's work is to manage memory like which folder is presend or which options are in which memory.
    3. Process Management → Everything is a processs in the computing memory management. if you are playing a song it's a proces, doing some work is a process these things comes as a part of process management.
    
    ---
    
    Libraries
    
    ---
    
       c/c++ libraries, interface throgh java, surface manager handling Ui windows, 2D and 3D grapics, Media, codecs, SQLite, browser engine all comes into libraries.
    
    to make it very simple some standard things that are being followed or some standard procedure that are being followed are their for the purpose of devloeper to simply their work we had build libraries.
    
    ---
    
    Android applicaion Framework
    
    ---
    
    - it's basically a API interface
        - Work is to manage the entire appcliation in the single way like framework have activity manager, content provider, package manager etc. these manager combines to form a framework we as developer use this to get our work done.
        - it's contains all the applcaition component i.e acitivty manager, content provider
    
- What are the Various Storage that Android Provides?
    
    SharedPreferences 
    
    - Shared Preferences → it is used to store data in key-value pairs and you can easily access it from the SharedPreferences interface.
        - Shared preferences as a data store are used when you can store your data in key-value pairs in the application
        - When you need this data to stay even when the app is closed, for example, user preferences of the application.
        - Suppose, you have a weather application that you built and you allow your user to select the unit degree Celsius or Fahrenheit as a preference in the application. And you don’t want the user to select it every time when he opens your awesome weather application. This can be a good opportunity to use Shared Preferences to store user preferences in key-value pairs.
    - SQLite → Provides a  structured data store and you can use it to store private data in an android applicatoin.
        - SQLite is used to store more structured data locally in the mobile application, it is used to store structured data like your store in an RDBMS,
        - it provides similar features to MySQL or any other SQL database but with limited functionality. Some features like stored procedures are not available. SQLite is very helpful when you would like to store complex data in your android application or a large amount of data that can be used by the application to provide a better user experience.
    - File Storage → used to store raw files in sd card or memory card, storing mp3 files for music,etc.
        - In Android applications, we can choose to use the device storage space in order to store the data in it for the application we build. This type of storage is useful when the data is like an image, audio, video, or a file like that. These files don’t need to be searched internally and can be accessed in the app for storing large files. The application should be able to parse this data in order to use this while running though. Like you will need a video player specific to the format you’re storing the file in the device if it’s not supported by your Android device.
        - There can be two options here one is internal storage and the other is external storage, I recommend external storage as people have a large amount of external storage on their phones generally as they use an SD card in their devices.
        - Though an option can be provided in this case to the user if they would like to store the files in their internal phone storage or external storage.
    - Content Providers → used to store semi-structured data with user-configurable data access.
        
        Suppose you have an application which provides data to other applications on the device, you store about 5 rows in a database including:
        
        email, name, phone number, profile photo and password
        
        But to other applications, you would only like to expose a part of this information which is you can assume only the profile picture of the user.
        
        In this scenario, content providers can help you out and you can use them in order to achieve this. Content Providers can help you with restricting the data access for all the data you have but providing access to the data you want other apps to access in your device.
        
    - Cloud Storage → used to store data in third-party data stroage, for example google drive.
        
        You can use cloud storage and access it through various APIs provided by Microsoft, Google and other companies. This can help you back up your application data on the internet which can be restored in case you lost your device and got a new one. For example, WhatsApp allows you to store your device backup in google drive.
        
- What is a Singleton Class in Android?
    - A class that can have only one object at a time.
    - After first time, if we try to instantiate the Singleton class, the new variable also points to the first instance created.
    - So whatever modifications we do to any variable inside the class through any instance, it affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined.
- What is AAPT?
    - AAPT stands for Android Asset Packaging Tool. It is a build tool that gives the ability to developers to view, create, and update ZIP-compatible archives (zip, jar, and apk). It parses, indexes, and compiles the resources into a binary format that is optimized for the platform of Android
    - `aapt` is about Android **resources** like `.xml` etc
    
    > AAPT stands for Android Asset Packaging Tool. The Android Asset Packaging Tool (aapt) takes your application resource files, such as the AndroidManifest.xml file and the XML files for your Activities, and compiles them.This is a great tool which help you to view, create, and update your APKs (as well as zip and jar files). It can also compile resources into binary assets. It is the base builder for Android aplications. This tool is a piece of the SDK (and assemble framework) and permits you to see, make, and redesign Zip-perfect chronicles (zip, jolt, apk)
    > 
    
    You can find it
    
    ```kotlin
    ..\\android-sdk\\build-tools\\<buildToolsVersion>
    ```
    
    1. `aapt package`, `aapt add` - Building Android Application Bundles (APKs)
    2. `aapt dump` - Dumping information from an APK file via:
    - read a VersionCode
    - aapt dump badging <name>.apk
    - Check Your Permissions
    - aapt dump permissions <name>.apk
    
    Also `aapt` take care of resources in ProGuard process[[About]](https://stackoverflow.com/a/59285427/4770877)Read more [here](https://www.anexinet.com/blog/android-what-is-aapt/), [here](https://spin.atomicobject.com/2011/08/22/building-android-application-bundles-apks-by-hand/), [here](https://crushingcode.nisrulz.com/whats-in-the-apk/)
    
- What is the Difference between MVVM and MVP & MVC?
    
    Need of architecture
    
    - Scalability & Maintainability of an application
    - To achieve this we implement architecutre patterns
        - Seperation of concers
        - Unit testing
    - MVC
        
        Model-View-Controller
        
        View (xml) → controllder(activity) → Model(data class, Pojo)
        
    - MVP
        
        VIEW(xma) activity/fragment → PRENSENTER( simple class presentation logic) → MODEL (data classes, pojo etc)
        
    - MVVM
        
        Model → View → View Model
        
- Memory Leak
    
    for java
    
    - For languages
        - Memory leak occurs when programmers create a memory in heap and forget to delete it.
        - The consequences of memory leak is that it reduces the performance of the computer by reducing the amount of available memory. Eventually, in the worst case, too much of the available memory may become allocated and all or part of the system or device stops working correctly, the application fails, or the system slows down vastly .
        - To avoid memory leaks, memory allocated on heap should always be freed when no longer needed.
    - For Android Studio
        
        Garbage Collector is not able to free up memory from objects that are not needed anymore
        
    - Curious Case of Memory Leak
        
        e.g If you had an activity and you created an object inside it when you rotate the screen object won't be destroyed as object holds reference to activity and that object will not allow activity to be eligible for garbage collection. If we rotate the application severral times then every time newInstance will be created old remains the same this lead to the situation mentioned below
        
        - Activity is liviing beyond it's expected lifecycle and this is called as memory leak
        - As time progresses, this will comsume all memory
        - Pretty soon app will run out of memory → the app performance degrads and then app get crashed.
    - Finding Memory Leak
        
        In andriod studio you can find Profiler select memory and click on the heap dump one you select heap dump it will open 'hprof' file automatically so  select android/fragment leak
        
    - Finding Memory Leak Quicker way using Leak Canary
        - Add LeakCanery depency
        - Create a custom Android Application Class
        - Initialize LeakCanary RefWatcher Instace ( clas in leak canary)
        - Activity is a Context and activity is the subclassl of the context
        - Context is the super class of all other context. Context Wrapper (it's the implementation of the context class )
        - ContentProvider.getContext(), Context.getApplicationContext() these all refer to the applicationContext and not creating the new instance of the context that's why when in case of this when we are using the getAppicatoin context the it's not crating the another one it is simply giving the existing one.
        - Everytime activity gets created (due to screen rotation) - no new instances of context are getting created
    - Unraveling Context
        
        
- Java References
    
    Java has 4 References Types
    
    1. Strong (normal)
    2. Soft
    3. Weak → eligible for garbage collection by GC (Garbage Collector)
    4. Phantom 
- DeadLocks
    
    Deadlock in Java is a part of multithreading. Deadlock can occur in a situation when a thread is waiting for an object lock, that is acquired by another thread and second thread is waiting for an object lock that is acquired by first thread. Since, both threads are waiting for each other to release the lock, the condition is called deadlock.
    
- Dependencies injection in Android
    - Adavatages of using Dependency-Injection
        1. Reusability of code
        2. Ease of refactoring
        3. Ease of Testing
        4. Helps to make dagger code easy and simple for developer
    - Hilt-Annotation
        1. @HiltAndroidApp → It triggers Hilt's code generation, including a base class for your application that serves as the application-level dependency container.
        2. @AndoirdEntryPoint → Hilt provides dependencies to other android classes that have this annotation. This component can recieve dependencies from their respective parent classes.
        3. @Inject to obtain dependencies from a component use this annotation to perform field injection.
        4. @Module → it informs hilt how to provide instances of certain types.
        5. @InstallIn → To tell hilt which andriod class each module will be used or installed in.
        6. @Provides → 
            1. This function tells hilt what type of instances this fuctions provides.
            2. function body tells hilt how to provide an instance of the corresponding type.
        7. @Singleton → We are providing this annotation states the result that whenever the componet needs to provide an instance of `ApiClientServic` it provides the same instance everytime. 
    - Understanding Dagger
        1. @Module → it’s a provider of dependency and using this annotation will make dagger understand that this is a module.
        2. @HiltAndroidApp → it generates all the component classes which we have to do manually using Dagger.
        3. @Inject  → it will helping passing the dependency required class in the constructor itself.
        4. @Provide → To inject everything into the constructor we use this annotation and we also provide dependencies using this annotation and which would be accessed across the application.
        5. @InstallIn → this annotation is to install it in SingletonComponent. SingletonComponent is provided by Dagger-Hilt.
        6. @Singleton → helps the instance to be created and used once across the app.
        7. @AndroidEntryPoint → to make any Android Class supported by Dagger-Hilt we use this annotation. means dagger can now inject dependencies in this class.
- Project Structure of Android Application?
    - Module
        
        A module is a collection of source files and build settings that allows you to divide your project in discrete units of functionality. Your project may have one or more module and one module can may use another module as dependency. Each module can easily build, tested and debugged.
        
        1. Android app Module
        2. Feature Module
        3. Library Modle
            - Android Library: This type of library can contain all file types supported in an Android project, including source code, resources, and manifest files. The build result is an Android Archive (AAR) file that you can add as a dependency for your Android app modules.
            - Java Library: This type of library can contain only Java source files. The build result is an Java Archive (JAR) file that you can add as a dependency for your Android app modules or other Java projects.
        4. Google Cloud Module
    - Project Files
        
        By default we can see the project files into the Andorid view.
        
        - Show all project build-related configurations files in a top-level Gradle Script group.
        - Shows all manifest files for each module in a module-level group
        - Shows all alternative resource files in a single group, instead of in separate folders per resource qualifier.
        
        manifests
        
        java
        
        res
        
        The Android Project View.
        
        ```kotlin
        
        When you select Project view, you can see a lot more files and directories. The most important of which are the following:
        
        module-name/
        
        build/
        Contains build outputs.
        
        libs/
        Contains private libraries.
        
        src/
        Contains all code and resource files for the module in the following subdirectories:
        
        androidTest/
        Contains code for instrumentation tests that run on an Android device. For more information, see the Android Test documentation.
        
        main/
        Contains the "main" sourceset files: the Android code and resources shared by all build variants (files for other build variants reside in sibling directories, such as src/debug/ for the debug build type).
        
        AndroidManifest.xml
        Describes the nature of the application and each of its components. For more information, see the AndroidManifest.xml documentation.
        
        java/
        Contains Java code sources.
        
        jni/
        Contains native code using the Java Native Interface (JNI). For more information, see the Android NDK documentation.
        
        gen/
        Contains the Java files generated by Android Studio, such as your R.java file and interfaces created from AIDL files.
        
        res/
        Contains application resources, such as drawable files, layout files, and UI string. See Application Resources for more information.
        
        assets/
        Contains file that should be compiled into an .apk file as-is. You can navigate this directory in the same way as a typical file system using URIs and read files as a stream of bytes using the AssetManager . For example, this is a good location for textures and game data.
        
        test/
        Contains code for local tests that run on your host JVM.
        
        build.gradle (module)
        This defines the module-specific build configurations.
        
        build.gradle (project)
        This defines your build configuration that apply to all modules. This file is integral to the project, so you should maintain them in revision control with all other source code.
        For information about other build files, see Configure Your Build.
        
        Project structure settings
        To change various settings for your Android Studio project, open the Project Structure dialog by clicking File > Project Structure. It contains the following sections:
        
        SDK Location: Sets the location of the JDK, Android SDK, and Android NDK that your project uses.
        
        Project: Sets the version for Gradle and the Android plugin for Gradle, and the repository location name.
        
        Modules: Allows you to edit module-specific build configurations, including the target and minimum SDK, the app signature, and library dependencies. 
        See Modules, below.
        
        Modules
        The Modules settings section lets you change configuration options for each of your project's modules. Each module's settings page is divided into the following tabs:
        
        Properties: Specifies the versions of the SDK and build tools to use to compile the module.
        Signing: Specifies the certificate to use to sign your app.
        Flavors: Lets you create multiple build flavors, where each flavor specifies a set of configuration settings, such as the module's minimum and target SDK version, and the version code and version name. For example, you might define one flavor that has a minimum SDK of 15 and a target SDK of 21, and another flavor that has a minimum SDK of 19 and a target SDK of 23.
        Build Types: Lets you create and modify build configurations, as described in Configuring Gradle Builds. By default, every module has debug and release build types, but you can define more as needed.
        Dependencies: Lists the library, file, and module dependencies for this module. You can add, modify, and delete dependencies from this pane. For more information about module dependencies, see Configuring Gradle Builds.
        ```
        
- App  Manifest Overview?
    - Manifest file describe the essential information about your app to the android build tools, Android operating system and Google play
    - The AndroidManifest.xml file contains information regarding the application that the Android system must know before the codes can be executed.
    - This file is essential in every Android application.
    - It is declared in the root directory.
    - This file performs several tasks such as:
        - Providing a unique name to the java package.
        - Describing various components of the application such as activity, services, and many more.
        - Defining the classes which will implement these components
    
    File Features:- 
    
    - Package Name and application ID
    - App Components
    - Intent-filters
    - Local labels
    - Permissions
    - Device Compatibiility
    - <user-sdk>
- Activity and it's Lifecycle?
    - Screen which is shown to the user.
    
    Lifecycle
    
    - onCreate → open an app and activity it calls the first it's like the constructor of the class
    - onStart → when user can see the screen
    - onResumt → when user can interact the screen
    - onPause  → when part of app is visible but in background
    - onStop → when app is not visible to the user
    - onDestroy →  when activity is destroyed.
    - OnRestart → called when we navigate back to the activity.
    
    Scnario → 
    
    1. lock button clicked 
        1. ( onPause → onStop )
        2. open ( onRestart → onStart → onResume )
    2. Pressing Home Button 
        1. presses home (onPause → onStop )
        2. Reopen (onRestart → onStart → onResume)
    3. kill app ( onPause → onStop → onDestroy) 
    4. Setting permissions ( onRestart → permiss → onResume)
    5. checking login status 
        1. onStart ( login) onStop (logout)
    6. youtube pause video 
        1. if you want to pause the music then pause it in onPause method
        2. resume video in the onResume method
    7. Weather app
        1. fetch data (onstart)
    
- **When only onDestroy is called for an activity without onPause() and onStop()?**
    - when we write finish in the onCreate method then it will directly call onDestroy method.
- **Why do we need to call setContentView() in onCreate() of Activity class?**
    
    as onCreate method called only once. So most of the initialization completed in the onCreate method. And if we write setContentView() in another method then those method called more than once. so to make it efficient we call it in the onCreate method.
    
- What is the difference between FragmentPagerAdapter and FrgmentStatePagerAdapter?
    - FragmentPagerAdapter → Each fragment visisted by the user will be stored in the memory but the view will be destroyed. When the page is revisited the view will be created not the the instance of the fragment.
    - FragmentStatePagerAdapter → Here, the fragment instance will be destroyed when it is not visible to the user, except the saved state of the fragment.
- How to communicate between fragment?
    
    Fragment Communcation should be done directly. There are two ways of doing so.
    
    1. With the help of ViewModel
    2. With the help of Interface
    
    ```kotlin
    
    /**Passing data through interface */
    class FragmentA : Fragment() {
    
        lateinit var mCallback: TextClickedListener
    
        //defining Interface
        interface TextClickedListener {
            fun sendText(text: String)
        }
    
        fun setOnTextClickedListener(callback: TextClickedListener) {
            this.mCallback = callback
        }
    
        fun yourMethodofSendingText() {
            //here you can get the text from the edit text or can use this method according to your need
            mCallback.sendText("YOUR TEXT")
        }
    
    }
    
    class MainActivity :Activity(), FragmentA.TextClicked {
        fun onAttachFragment(fragment: Fragment) {
            if (fragment is FragmentA) {
                fragment.setOnTextClickedListener(this)
            }
        }
        override fun sendText(text: String) {
            // Get FragmentB
            val callingFragment = getSupportFragmentManager().findFragmentById(R.id.fragment_b) as FragmentB
            //calling the updateText method of the FragmentB
            callingFragment.updateText(text)
        }
    }
    
    class FragmentB : Fragment() {
    
        fun updateText(text: String) {
            // Here you can perform the required action
            //this  action can be updating the text of the TextView with the "text" string
            //or any relevant action
        }
    }
    ```
    
- Views & ViewGrounp?
    
    View → A view is a super class for all the UI Components
    
    Viewgroup → A group of view is known as ***ViewGroup***
    
    **Width and Height of a View**
    
    1. **wrap_content:** This will wrap the content of a view. ***For example***, if you are using LinearLayout and the LinearLayout consists of two buttons and you are using the height of the LinearLayout as wrap_content, then the height of the LinearLayout will be equal to the length under which both the buttons are present i.e. the LinearLayout is wrapping the contents present in it.
    2. **match_parent**: If a view is using match_parent, then it will get the same size as its parent is having. ***For example***, if LinearLayout is the parent view and the height of LinearLayout is 80dp, then if we are using Button inside the LinearLayout with height as match_parent, then the height of the Button will also be 80dp i.e. matching the parent.
    
    Resources
    
    - **Drawable:** here, we put all our graphics, vector images, custom drawings.
    - **Layout** - here, we put all our screen layout files. example: *activity_main.xml*
    - **Mipmap** - here, we put the images which are used to make the logo of the application.
    - **Values** - this folder contains four default files. colors.xml, dimens.xml, strings.xml, style.xml.
    
    Sizes
    
    → What the difference between sp and dp ?
    
    - Sp is similar to the DP unit but additionally it is also scaled according to the font size preference of the user.
    - DP is an abstract or virtual unit which is based on the physical density of the screen. One DP means one pixel on a 160 dpi screen.
    - For text size, we use "**sp**" (**Scale Independent Pixels).**
    - For views other than text, we use "**dp**" (**Density Independent Pixel).**
    - **ldpi:** resources of low-density (~ 120dpi)
    - **mdpi:** resource of medium-density (~ 160dpi)
    - **hdpi:** resources of high-density (~ 240dpi)
    - **xhdpi:** resources of extra-high-density (~ 320dpi)
    - **xxhdpi:** resources of extra-extra-high-density (~ 480dpi)
    - **xxxhdpi:** resources of extra-extra-extra-high-density (~ 640dpi)
- Difference between View.Gone and View.Invisible
    
    View.Gone → View is invisible and It will not take the space for layout purposes.
    
    View.Invisible → The view is invisible, but it still takes up the space for the layout purposes. 
    
- Why Fragment shoud not directly communicate with each other?
    - Well, with Fragments you aren't always sure if they will be alive and attached at the time of communication. Whether Fragments are attached and available or not might also depend on device layout or size. If you're absolutely sure that your Fragments will both be attached to your activity and available at the same time, then I suppose you can communicate directly.
    - Having said that, Fragments are meant to be logical, standalone units. From the docs:
    
    ```
    You can think of a fragment as a modular section of an activity
    
    ```
    
    - It kind of breaks the model if the fragments are affecting each other directly.
    - Why not rather define an interface in your Activity and get Fragment A to call a method in the Activity? Then your Activity can check whether Fragment B is available and can then call the appropriate function in Fragment B.
    - [Here](http://developer.android.com/guide/components/fragments.html#EventCallbacks) is the docs suggestion
- Can we create our own view's
    
    Yes we can create our own views It's just a way an android developer a painter
    
    for more details [refer this](https://blog.mindorks.com/create-your-own-custom-view) 
    
- Stack Views
    
    **StackView** is a widget that helps in arranging the items in the form of stacked cards. Whenever we flip the front item, the next item from behind comes to the front.
    
    For More details [Refer this](https://www.geeksforgeeks.org/stackview-in-android/#:~:text=StackView%20is%20a%20widget%20that,to%20do%20in%20this%20article.) 
    
- ListView and RecyclerView Difference
    
    [https://stackoverflow.com/questions/26728651/recyclerview-vs-listview](https://stackoverflow.com/questions/26728651/recyclerview-vs-listview)
    
- What is Viewholder Patterns and why should we use it ?
    
    `ViewHolder` design pattern is used to speed up rendering of your ListView - actually to make it work smoothly. Your code might call findViewById() frequently during the scrolling of ListView, which can slow down performance. Even when the Adapter returns an inflated view for recycling, you still need to look up the elements and update them.
    
    A way around repeated use of findViewById() is to use the "view holder" design pattern, to hold the references to view elements for caching purposes. ViewHolder struct is stored in the target convert view via View.setTag(). When recycling a View, we can get the ViewHolder cache by (ViewHolder) convertView.getTag().
    
- RecyclerView Optimization - Scrolling *
    1. Use Image-Loading Library
    2. Set image width and height.
        1. If our image width and height are dynamic(not fixed), and we are getting the `imageUrl` from the server.
        2. If we do not set the correct image width and height prior, the UI will **flicker** during the transition of loading(downloading of image) and setting of the image into the ImageView(actually making it visible when downloading completes).
- How android image loading library Glide and Fresco work internally?
    - Problems we faced while loading an image into an imageview
        1. OOM - out of memory error.
        2. Slow loading of an image into the view.
        3. Ui becomes unreponsive. Not smooth scrolling.
    - OOM( Out of memory error )
        - To resolve this issue Glide come up with Downsampling means scaling the bitmap( image ) to a smaller size which is actually required by the view, Let's say we have an image of size 400 * 400 so why to load an image of 2000 * 2000, Glide down-samples the bitmap to 400 * 400 and then show it in the view.
        
        `GlideApp.with(context).load(url).into(imageView);`  
        
        - Glide know the dimensions of the imageView as it taked the imageView as a parameter.
        - Glide down-samples the image without loading the whole image into the memory. This way, the bitmap takes less memory, and the out of memory error is solved. And we all are happy.
    - Slow loading
        - Slow loading is another problem when it comes to loading a bitmap into the view. One of the major reason of slow loading is that we do not cancel the task like downloading, decoding a bitmap even when the view is out of the window, hence there are many tasks which are being done even though we do not need, so it takes time for the actual image to load which just came in the window. Glide takes care of this, it cancels all the tasks properly and only loads the images which are visible to the user. This is one way to make loading fast.
        - Glide is aware of the activity, fragment lifecycle, this way it knows which image downloading tasks need to be canceled
        - It maintains two levels of caching:
            1. Memory Cache
            2. Disk Cache
            
    - When we provide an url what happens?
        1. Check if image with url key available in memory cache or not.
        2. if present in the memory cache it just shows the bitmap by taking it from the memory cache.
        3. if not then it check the disk cache, if present in the disk cache it loads the bitmap from the disk, also put it in the memory cache and load the bitmap into the view.
        4. if not present in the disk cache, it downloads the image from the network, puts it in the disk view and also put it in the memory cache and load the bitmap into the view.
        
        This way it makes loading fast as showing directly from the memory cache is always faster.
        
    - Unresponse UI
        - Reason
            - Application is doing too many tasks on the main thread. As we know that all the tasks related to rendering UI are done in the main thread. And the android updates the UI in every 16 ms if you do any task that takes more than 16ms then android has to skip that update and hence skip that frame. So skipping frame leads to less frame per second.
            
            `More FPS more smothness` 
            
            if FPS is lower the user sees the UI laggy and that is unresponsive.
            
            - While loading the bitmaps, even if we load those in the background, then also the UI lags. Why?
            
            - The reason is that the bitmaps are larger in size, it makes the Garbage Collector(GC) run very frequently.
            - The basic rule is that — **The time for which GC is running, your application is not running**.
            
            `GC takes the time to run and it forces the system to skip many frames. So, GC is the main culprit.`
            
        - How does Glide solve this.
            
            `Using Bitmap Pool.`
            
            - Glide uses this bitmap pool concept to reduce GC calls as much as possible.
            - By using the Bitmap pool, it avoids continuous allocation and deallocation of memory in your application, reduces GC overhead, which results in a smooth-running application.
            - How to avoid continuous allocation and deallocation of memory in your application?
            - By using the [inBitmap](https://developer.android.com/reference/android/graphics/BitmapFactory.Options.html#inBitmap) property of the bitmap. (which reuses bitmap memory).
            - Suppose we have to load a few bitmaps in an Android application.
            - Let say we have to load two bitmaps (bitmapOne, bitmapTwo) one by one. When we load bitmapOne, it will allocate the memory for bitmapOne. Then if when we no longer need bitmapOne, do not recycle the bitmap (as recycling involves calling GC). Instead, use this bitmapOne as an [inBitmap](https://developer.android.com/reference/android/graphics/BitmapFactory.Options.html#inBitmap) for bitmapTwo. This way, the same memory can be reused for bitmapTwo.
            - Let’s see the code, how it works. See the [inBitmap](https://developer.android.com/reference/android/graphics/BitmapFactory.Options.html#inBitmap) property carefully.
            
            ```kotlin
            Bitmap bitmapOne = BitmapFactory.decodeFile(filePathOne);
            imageView.setImageBitmap(bitmapOne);
            // lets say , we do not need image bitmapOne now and we have to set // another bitmap in imageViewfinal BitmapFactory.Options options =new BitmapFactory.Options();
            options.inJustDecodeBounds =true;
            BitmapFactory.decodeFile(filePathTwo, options);
            options.inMutable =true;
            options.inBitmap = bitmapOne;
            options.inJustDecodeBounds =false;
            Bitmap bitmapTwo = BitmapFactory.decodeFile(filePathTwo, options);
            imageView.setImageBitmap(bitmapTwo);
            ```
            
            - So, we are reusing the memory of bitmapOne while decoding the bitmapTwo.
            - This way we are not allowing the GC to be called again and again as we are not leaving off the reference of the bitmapOne, instead we are loading the bitmapTwo in the memory of bitmapOne.
            - One important thing is that the size of the bitmapOne should be equal or greater than the bitmapTwo so that bitmapOne’s memory can be re-used.
            - There are a few things which are very specific to different Android versions which are to be considered while re-using the bitmap memory, I suggest you read [this project](https://github.com/amitshekhariitbhu/GlideBitmapPool).
            
            So, Glide creates a bitmap pool of bitmaps.
            
            - You can say that the bitmap pool is a list of bitmaps that are no longer needed but are available for reuse to load the new bitmap in the same memory.
            - When any bitmap is available for recycle, Glide just pushes the bitmap in that bitmap pool.
            - When Glide has to load the new bitmap, it just gets a bitmap that can be reused to load the new one to reuse the same memory from that bitmap pool. Hence no recycling, no GC calls.
            
            Fresco also does the same things as Glide. There are a few different things but the concept is almost the same.
            
- What is memory cache and disk cache
    - Memory Cache: It keeps the data in the memory of the application. If the application gets killed, the data is evicted. Useful only in the same session of application usage. Memory cache is the fastest cache to get the data as this is in memory.
    - Disk Cache: It saves the data to the disk. If the application gets killed, the data is retained. Useful even after the application restarts. Slower than memory cache, as this is I/O operation.
- Dialog
    
    A dialog is a small window that prompts the user to make a decision or enter additional information. A dialog does not fill the screen and is normally used for modal events that require users to take an action before they can proceed.
    
- What is the difference between Dialog and Dialog fragment?
    - **Dialog:** A dialog is a small window that prompts the user to make a decision or enter additional information.
    - **DialogFragment:** A DialogFragment is a special fragment subclass that is designed for creating and hosting dialogs. It allows the FragmentManager to manage the state of the dialog and automatically restore the dialog when a configuration change occurs.
- Intents
    - What are Intents?
        
        An Intent is a messaging object you can use to request an action from another app componet.
        
        or 
        
        Intents as a messaging service that is used to communicate between various components of the Android application
        
    - Intent Types
        - Explicit Intents
            - Used to communicate between the application only, used to communicate with a particular component of the same application.
            - For example, if you want to launch an Activity by clicking some button on the present Activity then you can specify the fully-qualified address of the desired Activity to launch that Activity. Since this approach requires a fully-qualified address, so, you can use this approach in your own application i.e. you can use Explicit Intents to have communication in your own application.
        - Implicit Intents
            - Here, you don’t need to specify the fully-qualified address. All you need to do is just specify the action that is to be performed by an Intent. By using the Implicit Intents you can communicate between various applications present in the mobile device.
            - For example, you can access the current location by accessing the location data from other application also i.e. if one application A is detecting the current location of the user then you can use the data of the user i.e. the current location by communicating with application A.
        
        If you call the Implicit Intent then, the Android System will search for all the available components that can be used to start that activity. This process is done by comparing the contents of the intent with the content present in the ***intent-filter*s** declared in the ***AndroidManifest.xml*** file. If there is only one intent-filter that is compatible with the content of the intent then the Android system will start the desired component. But if there are a number of ***intent-filters*** that are compatible with the content of the Intent then the Android System will show you a list of application that can be used to perform that particular action. For example, if you want to share some image from the Gallery, then you will get a number of choices like WhatsApp, Facebook, Instagram, Shareit, Gmail and many more image sharing application. Now, you can choose any of the available choices.
        
    - Use cases of Intent
        - Starting an Activity
            
            You can use the Intents to start a particular activity by using Intents. For example, if you are having two activities namely **LoginActivity** and **MainActivity** then, you can start the **MainActivity** by clicking the login button present on the **LoginActivity**. By using the ***startActivity()***, you can start the desired Activity using the Intents.
            
        - Starting a Service
            
            You can think of **service** as a component that will perform a particular task in the background. So, you can use Intents to start a service also. For API level 21 or higher, you can use [JobScheduler](https://developer.android.com/reference/android/app/job/JobScheduler.html) to start a service. For API level lower than 21, you can use the Service class to achieve the same.
            
        - Delivering a broadcast
            
            A broadcast is a message that is received by the application from the system. A very common example of a broadcast can be **Device Charging** message. So, you can use a broadcast to send some kind of message to the applications present in the device. This is done by passing an Intent to [sendBroadcast()](https://developer.android.com/reference/android/content/Context.html#sendBroadcast%28android.content.Intent%29) or to [sendOrderedBroadcast()](https://developer.android.com/reference/android/content/Context.html#sendOrderedBroadcast%28android.content.Intent,%20java.lang.String%29).
            
    - Information present in Intent
        
        Basic informataion which intent contains are
        
        1. Actions → An action is a string that specifies the action to be performed by a particular Activity. e.g ACTION_SEND used to share some data with another app like email app.
        2. Data → While creating an Intent, you can pass the data and the type of data on which the action is to be performed by the Android System with the help of Intents. The URI object is used to reference the data that will be used to perform some action on it.
        3. Category → it is used in case of Explicit Intents where you need to specify the type of application that will be used to perform a particular action.
        4. Component Name → The component name is the name of the component that is to be started. You can set the component name byusing ***setComponent()*** or ***setClass()*** or with the Intent Constructor.
        5. **Extras:** You can add extra data to an Intent in the form of key-value pairs and this extra information can be passed from one Activity to the other. ***putExtra()*** is used to add some extra data to the Intents and this method accepts two parameters i.e. the key and its corresponding value.
    - Example of Intent
        
        Explicit Intent
        
        ```kotlin
        // Executed in an Activity, so 'this' is the Context// The fileUrl is a string URL, such as "http://www.example.com/image.png"
        val downloadIntent = Intent(this, DownloadService::class.java)
        downloadIntent.data = Uri.parse(fileUrl)
        startService(downloadIntent)
        ```
        
        Implicit Intent
        
        ```
        // Create the text message with a string
        val sendIntent = Intent().apply {
            action = Intent.ACTION_SEND
        putExtra(Intent.EXTRA_TEXT, textMessage)
            type = "text/plain"
        }
        
        // Verify that the intent will resolve to an activityif (sendIntent.resolveActivity(packageManager) !=null) {
            startActivity(sendIntent)
        }
        ```
        
    - Register an activity as browser.
        
        ```kotlin
        <activity android:name=".BrowserActivitiy"
                  android:label="@string/app_name">
          <intent-filter>
             <action android:name="android.intent.action.VIEW" />
             <category android:name="android.intent.category.DEFAULT" />
             <data android:scheme="http"/>
          </intent-filter>
        </activity>
        ```
        
    - Data Transfer to the target Component
        
        ```kotlin
        val intent = Intent(this, ActivityTwo::class.java)
        intent.putExtra("Value1", "Value 1here")
        intent.putExtra("Value2", "Value 2here")
        ```
        
        The first parameter passed in the ***putExtra()*** is the key and the second parameter is its value.
        
        ```kotlin
        val data = intent.extras
        if (data ==null) {
        return
        }
        val value1 = data.getString(Intent.EXTRA_TEXT)
        if (value1 !=null) {
        // do something with the data
        }
        ```
        
    - Forcing an app Chooser
        
        ```kotlin
        val sendIntent = Intent(Intent.ACTION_SEND)
        ...
        
        // Always use string resources for UI text.// This says something like "Share this photo with"
        val title: String = resources.getString(R.string.chooser_title)
        // Create intent to show the chooser dialog
        val chooser: Intent = Intent.createChooser(sendIntent, title)
        
        // Verify the original intent will resolve to at least one activityif (sendIntent.resolveActivity(packageManager) !=null) {
            startActivity(chooser)
        }
        ```
        
    - **What is an Intent Filter?'**
        - Implicit intent uses the intent filter to serve the user request.
        - The intent filter specifies the types of intents that an activity, service, or broadcast receiver can respond.
        - Intent filters are declared in the Android manifest file.
        - Intent filter must contain <action>
        - Tells android which activities can handle which actions. This process is know as intent Resolution.
            - It tells android the activity can handle `ACTION_SEND`it also tells the type of data the activity can handle, intent filter must include a category of DEFAULT or it won't be able to receive implicit intents.
    - Sticky Intent?
        - Allows communication betweeen the function and a service.
        - sendStickyBroadcast() performs a sendBroadcast(Intent) known as sticky, i.e. the Intent you are sending stays around after the broadcast is complete, so that others can quickly retrieve that data through the return value of registerReceiver(BroadcastReceiver, IntentFilter).
        - For example, if you take an intent for ACTION_BATTERY_CHANGED to get battery change events: When you call registerReceiver() for that action — even with a null BroadcastReceiver — you get the Intent that was last Broadcast for that action.
        - Hence, you can use this to find the state of the battery without necessarily registering for all future state changes in the battery.
    - What is a pending Intent?
        - If you want someone to perform any Intent operation at future point of time on behalf of you, then we will use Pending Intent
        - A Pending Intent **specifies an action to take in the future**. It lets you pass a future Intent to another application and allow that application to execute that Intent as if it had the same permissions as your application, whether or not your application is still around when the Intent is eventually invoked.
- Bread Crumb Structure.
    
    It's usually the file navigation system that we see in the menu based UI
    
- What is Retofit and how does Retrofit Work internally?
    
    Before using any library we need to analyze three things **`What`**, **`Why`**  and **`How`**.
    
    - What
        
        Retofit is a type-safe HTTP client for Android and Java.
        
    - Why
        
        Retrofit make networking easier in Android Apps.
        
        As it has many features like easy to add custom headers and request types, file uploads, mocking responses, etc through which we can reduce boilerplate code in our apps and consume the web service easily.
        
    - How
        
        For Working with Networking we basically need 3 classes
        
        1. A model class which is used as a JSON model
        2. An interface that defines the HTTP operations needs to be performed.
        3. Retrofit.Builder class: Instance which uses the interface defined above and the Builder API to allow defining the **URL endpoint** for the **HTTP** operations. It also takes the **converters** we provide to format the **Response**.
- FLAG_ACTIVITY_NEW_TASK
- FLAG_ACTIVITY_CEAR_TASK
- When is a ViewModel destroyed? *
    
    `[ViewModel](https://developer.android.com/reference/androidx/lifecycle/ViewModel)` objects are scoped to the `[Lifecycle](https://developer.android.com/reference/androidx/lifecycle/Lifecycle)` passed to the `[ViewModelProvider](https://developer.android.com/reference/androidx/lifecycle/ViewModelProvider)` when getting the `[ViewModel](https://developer.android.com/reference/androidx/lifecycle/ViewModel)`. The `[ViewModel](https://developer.android.com/reference/androidx/lifecycle/ViewModel)` remains in memory until the `[Lifecycle](https://developer.android.com/reference/androidx/lifecycle/Lifecycle)` it's scoped to goes away permanently: in the case of an activity, when it finishes, while in the case of a fragment, when it's detached.
    
- Eveything About OOPS with implementation
    
    **OBJECT-ORIENTED PROGRAMMING SYSTEMS**
    
    **JAVA**
    
    **Object-Oriented Programming** is a methodology or paradigm to design a program using classes and objects. It simplifies the software development and maintenance by providing some concepts defined below :
    
    **Class** is a user-defined data type that defines its properties and its functions. Class is the only logical representation of the data. For example, a Human being is a class. The body parts of a human being are its properties, and the actions performed by the body parts are known as functions. The class does not occupy any memory space till the time an object is instantiated.
    
    **Object** is a run-time entity. It is an instance of the class. An object can represent a person, place, or any other item. An object can operate on both data members and member functions.
    
    Example 1:
    
    ```java
    class Student {
        String name;
        int age;
        public void getInfo() {
            System.out.println("The name of this Student is " + this.name);
            System.out.println("The age of this Student is " + this.age);
        }
    }
    ```
    
    ```java
    public class OOPS {
        public static void main(String args[]) {
            Student s1 = new Student();
            s1.name = "Aman";
            s1.age = 24;
            s1.getInfo();
            Student s2 = new Student();
            s2.name = "Shradha";
            s2.age = 22;
            s2.getInfo();
        }
    }
    ```
    
    Example 2:
    
    ```java
    class Pen {
        String color;
        public void printColor() {
            System.out.println("The color of this Pen is " + this.color);
        }
    }
    
    public class OOPS {
        public static void main(String args[]) {
            Pen p1 = new Pen();
            p1.color = blue;
            Pen p2 = new Pen();
            p2.color = black;
            Pen p3 = new Pen();
            p3.color = red;
            p1.printColor();
            p2.printColor();
            p3.printColor();
        }
    }
    ```
    
    **Note** : When an object is created **using** a new keyword, then space is allocated for the variable in a heap, and the starting address is stored in the stack memory.
    
    **‘this’ keyword :**  ‘this’ keyword in Java that refers to the current instance of the class. In OOPS it is used to:
    
    1. pass the current object as a parameter to another method
    2. refer to the current class instance variable
    
    **Constructor**: Constructor is a special method that is invoked automatically at the time of object creation. It is used to initialize the data members of new objects generally.
    
    - Constructors have the same name as class or structure.
    - Constructors don’t have a return type. (Not even void)
    - COnstructors are only called once, at object creation.
    
    There can be **three types** of constructors in Java.
    
    ```java
        /*
        1. Non-Parameterized constructor : A constructor which has no argument is known as a non-parameterized constructor(or no-argument constructor). It is invoked at the time of creating an object. If we don’t create one then it is created by default by Java.
         */
        class Student {
            String name;
            int age;
    
            Student() {
                System.out.println("Constructor called");
            }
        }
    
        /*
        2. Parameterized constructor : A constructor which has parameters is called a parameterized constructor. It is used to provide
            different values to distinct objects.
         */
        class Student {
            String name;
            int age;
    
            Student(String name, int age) {
                this.name = name;
                this.age = age;
            }
        }
    
        /*
        3. Copy Constructor : A Copy constructor is an **overloaded**
    constructor used to declare and initialize an object from another object. There is only a user defined copy constructor in Java(C++ has a default one too).
         */
        class Student {
            String name;
            int age;
    
            Student(Student s2) {
                this.name = s2.name;
                this.age = s2.age;
            }
        }
    ```
    
    **Note** : Unlike languages like C++, Java has no Destructor. Instead, Java has an efficient  garbage collector that deallocates memory automatically.
    
    **Polymorphism**
    
    Polymorphism is the ability to present the same interface for differing underlying forms (data types). With polymorphism, each of these classes will have different underlying data. Precisely, Poly means ‘many’ and morphism means ‘forms’.
    
    **Types of Polymorphism IMP**
    
    1. Compile Time Polymorphism (Static)
    
    2. Runtime Polymorphism (Dynamic)
    
    Let’s understand them one by one :
    
    **Compile Time Polymorphism** : The polymorphism which is implemented at the compile time is known as compile-time polymorphism. Example - Method Overloading
    
    Method Overloading : Method overloading is a technique which allows you to have more than one function with the same function name but with different functionality. Method overloading can be possible on the following basis:
    
    1. The return type of the overloaded function.
    
    2. The type of the parameters passed to the function.
    
    3. The number of parameters passed to the function.
    
    ```java
    class Student {
        String name;
        int age;
        public void displayInfo(String name) {
            System.out.println(name);
        }
        public void displayInfo(int age) {
            System.out.println(age)
        }
    
        public void displayInfo(String name, int age) {
            System.out.println(name);
            System.out.println(age);
        }
    }
    ```
    
    **Runtime Polymorphism** : Runtime polymorphism is also known as **dynamic polymorphism**. Function overriding is an example of runtime polymorphism. Function overriding means when the child class contains the method which is already present in the parent class. Hence, **the child class overrides the method of the parent class**. In case of function overriding, parent and child classes both contain the same function with a different definition. The call to the function is determined at runtime is known as runtime polymorphism.
    
    ```java
    class Shape {
        public void area() {
            System.out.println("Displays Area of Shape");
        }
    }
    
    class Triangle extends Shape {
    
        public void area(int h, int b) {
            System.out.println((1/2)*b*h);
        }
    }
    
    class Circle extends Shape {
        public void area(int r) {
            System.out.println((3.14)*r*r);
        }
    }
    ```
    
    **Inheritance**
    
    Inheritance is a process in which one object acquires all the properties and behaviors of its parent object automatically. In such a way, you can **reuse, extend or modify** the attributes and behaviors which are defined in other classes.
    
    In Java, the class which inherits the members of another class is called derived class and the class whose members are inherited is called base class. The derived class is the specialized class for the base class.
    
    Types of Inheritance :
    
    ```java
        /*
        1. Single inheritance : When one class inherits another class, it is known as single level inheritance
         */
    
        class Shape {
    
            public void area() {
                System.out.println("Displays Area of Shape");
            }
        }
    
        class Triangle extends Shape {
            public void area(int h, int b) {
                System.out.println((1 / 2) * b * h);
            }
        }
    
    /*
    2. Hierarchical inheritance : Hierarchical inheritance is defined as the process of deriving more than one class from a base class.
     */
    
        class Shape {
            public void area() {
                System.out.println("Displays Area of Shape");
            }
        }
    
        class Triangle extends Shape {
            public void area(int h, int b) {
                System.out.println((1/2)*b*h);
            }
        }
    
        class Circle extends Shape {
            public void area(int r) {
                System.out.println((3.14)*r*r);
            }
        }
    /*
    3. Multilevel inheritance : Multilevel inheritance is a process of deriving a class from another derived class.
     */
    
        class Shape {
            public void area() {
                System.out.println("Displays Area of Shape");
            }
        }
        class Triangle extends Shape {
            public void area(int h, int b) {
                System.out.println((1/2)*b*h);
            }
        }
        class EquilateralTriangle extends Triangle {
            int side;
        }
        /*
        4. Hybrid inheritance : Hybrid inheritance is a combination of
         */
    
    ```
    
    **Package in Java**
    
    Package is a group of similar types of classes, interfaces and sub-packages. Packages can be built-in or user defined.
    
    Built-in packages - java, util, io etc.
    
    import java.util.Scanner;
    
    import java.io.IOException;
    
    **Access Modifiers in Java**
    
    - **Private**: The access level of a private modifier is only within the class. It cannot be accessed from outside the class.
    - **Default**: The access level of a default modifier is only within the package. It cannot be accessed from outside the package. If you do not specify any access level, it will be the default.
    - **Protected**: The access level of a protected modifier is within the package and outside the package through child class. If you do not make the child class, it cannot be accessed from outside the package.
    - **Public**: The access level of a public modifier is everywhere. It can be accessed from within the class, outside the class, within the package and outside the package.
    
    ```java
    
    class Account {
        public String name;
        protected String email;
        private String password;
        public void setPassword(String password) {
            this.password = password;
        }
    }
    public class Sample {
        public static void main(String args[]) {
            Account a1 = new Account();
            a1.name = "Apna College";
            a1.setPassword("abcd");
            a1.email = "hello@apnacollege.com";
        }
    }
    ```
    
    **Encapsulation**
    
    Encapsulation is the process of combining data and functions into a single unit called class. In Encapsulation, the data is not accessed directly; it is accessed through the functions present inside the class. In simpler words, attributes of the class are kept private and public getter and setter methods are provided to manipulate these attributes. Thus, encapsulation makes the concept of data hiding possible.(**Data hiding**: a language feature to restrict access to members of an object, reducing the negative effect due to dependencies. e.g. "protected", "private" feature in Java).
    
    **Abstraction**
    
    We try to obtain an **abstract view**, model or structure of a real life problem, and reduce its unnecessary details. With definition of properties of problems, including the data which are affected and the operations which are identified, the model abstracted from problems can be a standard solution to this type of problems. It is an efficient way since there are nebulous real-life problems that have similar properties.
    
    In simple terms, it is hiding the unnecessary details & showing only the essential parts/functionalities to the user.
    
    Data binding **:** Data binding is a process of binding the application UI and business logic. Any change made in the business logic will reflect directly to the application UI.
    
    **Abstraction** is achieved in 2 ways :
    
    - Abstract class
    - Interfaces (Pure Abstraction)
    1. **Abstract Class**
    - An abstract class must be declared with an abstract keyword.
    - It can have abstract and non-abstract methods.
    - It cannot be instantiated.
    - It can have constructors and static methods also.
    - It can have final methods which will force the subclass not to change the body of the method.
    
    ```java
    abstract class Animal {
        abstract void walk();
        void breathe() {
            System.out.println("This animal breathes air");
        }
        Animal() {
            System.out.println("You are about to create an Animal.");
        }
    }
    class Horse extends Animal {
        Horse() {
            System.out.println("Wow, you have created a Horse!");
        }
        void walk() {
            System.out.println("Horse walks on 4 legs");
        }
    }
    class Chicken extends Animal {
        Chicken() {
            System.out.println("Wow, you have created a Chicken!");
        }
        void walk() {
            System.out.println("Chicken walks on 2 legs");
        }
    }
    public class OOPS {
        public static void main(String args[]) {
            Horse horse = new Horse();
            horse.walk();
            horse.breathe();
        }
    }
    ```
    
    2. **Interfaces**
    
    - All the fields in interfaces are public, static and final by default.
    - All methods are public & abstract by default.
    - A class that implements an interface must implement all the methods declared in the interface.
    - Interfaces support the functionality of multiple inheritance.
    
    ```java
    interface Animal {
        void walk();
    }
    
    class Horse implements Animal {
        public void walk() {
            System.out.println("Horse walks on 4 legs");
        }
    }
    
    class Chicken implements Animal {
        public void walk() {
            System.out.println("Chicken walks on 2 legs");
        }
    }
    
    public class OOPS {
        public static void main(String args[]) {
            Horse horse = new Horse();
            horse.walk();
        }
    }
    ```
    
    **Static Keyword**
    
    Static can be :
    
    1. Variable (also known as a class variable)
    2. Method (also known as a class method)
    3. Block
    4. Nested class
    
    ```java
    class Student {
    
        static Stringschool;
    
        String name;
    
    }
    
    public class OOPS {
    
        public static void main(String args[]) {
    
            Student.school= "JMV";
    
            Student s1 = new Student();
    
            Student s2 = new Student();
    
            s1.name = "Meena";
    
            s2.name = "Beena";
    
            System.out.println(s1.school);
    
            System.out.println(s2.school);
    
        }
    
    }
    ```
    
- **How does Kotlin work on Android?**
    
    Just like Java, the Kotlin code is also compiled into the Java bytecode and is executed at runtime by the Java Virtual Machine i.e. JVM. When a Kotlin file named `Main.kt` is compiled then it will eventually turn into a class and then the bytecode of the class will be generated. The name of the bytecode file will be `MainKt.class` and this file will be executed by the JVM.
    
- Everything about Gradle.
    - Defination with example ?
        - Gradle is a build system (open source) that is used to automate building, testing, deployment, etc. “build.gradle” are scripts where one can automate the tasks. For example, the simple task to copy some files from one directory to another can be performed by the Gradle build script before the actual build process happens.
        - *Gradle is an open-source build automation tool focused on flexibility and performance*
    - Why is Gradle Needed ?
        - Every Android project needs a Gradle for generating an apk from the *.java* and *.xml* files in the project.
        - Simply put, a gradle takes all the source files (java and XML) and applies appropriate tools, e.g., converts the java files into dex files and compresses all of them into a single file known as apk that is actually used.
    - Types if Build.gradle scripts
        - `Top-level build.gradle`
            
            ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-project-build-gradle.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-project-build-gradle.png)
            
            It is located at the root project directory and it's main function is to define the build configurations that will be applied to all the modules in the project.
            
            - *buildscript*
                - This block is used to configure the repositories and dependencies for gradle.
                - The repositories from which the dependencies for the project are to be downloaded (google and jcenter in this case) ( project dependencies downloaded)
            - *dependencies*
                - This block in buildscript is used to configure dependencies that the Gradle needs to build during the project.
                - The dependencies that are required at a project level (useful for all the sub-projects or modules). we can see that the Gradle dependency and the kotlin dependency are used throughout the project and hence it is declared here (at the project level).
            - *allprojects*
                - This is the block where one can configure the third-party plugins or libraries. For freshly created projects android studio includes mavenCentral() and Google’s maven repository by default.
                - The repositories for which all the sub-projects/modules are to be downloaded (google and jcenter in this case)
            - *task clean(type: Delete)*
                
                This block is used to delete the directory every time the project is run. This way the projects keep clean when someone modifies some config files like, during settings.gradle which requires a complete clean.
                
        - `Module-level build.gradle`
            
            ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-module-build-gradle.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-module-build-gradle.png)
            
            Located in the *project/module* directory of the project this Gradle script is where all the dependencies are defined and where the SDK versions are declared. This script has many functions in the project which include additional build types and override settings in the main/app manifest or *top-level build.gradle* file.
            
            1. We add the required plugins: the android Gradle plugin along with the kotlin plugins required
            - *android*
                
                This block is used for configuring the specific android build options.
                
                - *compileSdkVersion* – This is used to define the API level of the app and the app can use the features of this and lower level.
            - *defaultConfig*
                - *applicationId*– This is used for identifying unique id for publishing of the app.
                - *minSdkVersion*– This defines the minimum API level required to run the application.
                - *targetSdkVersion*– This defines the API level used to test the app.
                - *versionCode*– This defines the version code of the app. Every time an update needs to be of the app, the version code needs to be increased by 1 or more.
                - *versionName*– This defines the version name for the app. this could be increased by much while creating an update.
                1. The different build types that are to be included as per the requirement. You can learn more about build types [here](https://developer.android.com/studio/build/build-variants).
            - *buildTypes(release)*
                - *minifyEnabled*– this will enable code shrinking for release build.
                - *proguardFiles*– this will specify the **[progaurd](https://www.geeksforgeeks.org/how-to-use-proguard-to-reduce-apk-size-in-android/)** settings file.
                1. The different build types that are to be included as per the requirement. You can learn more about build types [here](https://developer.android.com/studio/build/build-variants).
            - *dependencies*
                
                This specifies the dependencies that are needed to build the project.
                
                1. Finally, all the third-party dependencies that are required for this respective module or sub-project.
    - What happens when the build proecess starts on Android Studio and click the Run Button
        
        ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-build-process.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-build-process.png)
        
        - compilers convert your source code into DEX (Dalvik Executable) files, which include the bytecode that runs on Android devices, and everything else into compiled resources.
        - The APK Packager combines the DEX files and compiled resources into a single APK. Before your app can be installed and deployed onto an Android device, the APK must be signed.
        - The APK Packager signs your APK using either the debug or release Keystore.
        - If you are building a debug version of your app, that is, an app you intend only for testing and profiling, the packager signs your app with the debug Keystore. Android Studio automatically configures new projects with a debug Keystore.
        - If you are building a release version of your app that you intend to release externally, the packager signs your app with the release Keystore.
        - To create a release Keystore, read about [signing your app in Android Studio](https://developer.android.com/studio/publish/app-signing#studio).
        - Before generating your final APK, the packager uses the [zipalign](https://developer.android.com/studio/command-line/zipalign) tool to optimize your app to use less memory when running on a device.
        - At the end of the build process, you have either a debug APK or release APK of your app that you can use to deploy, test, or release to external users.
    - Gradle Task
        
        ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-run-tasks.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-run-tasks.png)
        
        - Gradle is an action performed by Gradle. For example, when the run button is pressed in Android Studio, a Gradle task is triggered.
        - If we keep the build window open from the bottom navigation bar and click on the run icon, a list of the Gradle tasks can be observed on the console.
        
    - **Running Gradle tasks through the command line**
        
        Can we achieve the same behavior discussed in the Gradle tasks section through the command line? Yes, we can open the terminal from the bottom navigation bar and type:
        
        ```
        ./gradlew assembleDebug --console plain
        ```
        
        ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-terminal-run-tasks.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-terminal-run-tasks.png)
        
        We can see that this is the same set of tasks that we have observed from clicking the run button in Android Studio. Hence, the task that is triggered here by clicking the run button is “assembleDebug”.A description here from the command we have used;
        
        1. *./gradlew* means to use the Gradle Wrapper. It is highly recommended to always use the Wrapper version. You can understand more about the Gradle Wrapper [here](https://docs.gradle.org/current/userguide/gradle_wrapper.html)
        2. *assembleDebug* is the name of the task we just asked it to run.
        3. *-console* plain tells Gradle to print out the build log exactly as how you see it in Android Studio. It's completely optional to mention this.
        
        Similarly, if you want to view the list of Gradle tasks available, you can use the command:
        
        ```
        ./gradlew tasks
        ```
        
        You will be able to see a list of all the available Gradle tasks available:
        
        ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-tasks-comparision.png](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/gradle-for-android-tasks-comparision.png)
        
        We can also observe that the list of tasks displayed by executing the command from the terminal is similar to the tasks available in the Gradle console at the top right corner.
        
    - Creating Custom Tasks
        
        We have seen and understood how we can run the “assembleDebug” task from the command line. Now, what if we want to create our custom task: Let’s say we want to c
        
        lean the project by creating our custom task. We can add this task to the project-level build.gradle file:
        
        ```java
        taskclean(type: Delete) {
            delete rootProject.buildDir
        }
        ```
        
        Now when we provide on the terminal:
        
        ```java
        ./gradlew clean
        ```
        
        This executes the clean command that deletes the build directory as per the command given in the task declared. The same can also be obtained by selecting the option “Clean Project” under the “Build” menu. But if we wanted to customize our task, this is the way we can achieve it.
        
        Now this task is in a way default provided by Gradle at the project level build.gradle file. Now, let's consider one of the common use cases. Let's say once we build our apk through the assembleDebug process, we want to copy the apk to the Desktop and rename it to our own choice rather than keeping the 'app-debug.apk' name. How can we achieve this?
        
        Yes! By creating a custom Gradle task in the app level build.gradle file:
        
        ```java
        taskgetDebugAppInDesktopFolder(dependsOn: 'assembleDebug') {
            doLast {
                def destination = "Put the desired path"
                def desiredName = "Put the desired name"
                ext.apk = file("build/outputs/apk/debug/app-debug.apk")
        
        if (ext.apk.exists()) {
                    copy {
                        from ext.apk.absolutePath
                        into destination
                        rename { desiredName }
                    }
                }
            }
        }
        ```
        
        Here 'getDebugAppInDesktopFolder' is our task name, 'assembleDebug' is the task that our current Gradle task is dependent on. (assembleDebug is the task which builds our 'app-debug.apk') file. Finally, in our doLast block, we are getting the user name from the System properties so that this can be dynamic and copying the apk file if it exists on to the desktop.
        
        This makes our job easier rather than locating the 'app-debug.apk' file, copying it to our desktop and then renaming it.
        
- Mastering Proguard
    - What is Proguard?
        
        It's a free tool in Android, which helps us to do the following
        
        1. Shrink(Minify) the code → Remove unused code in the project.
        2. Obfuscate the code → Rename the names of class, field etc.
        3. Optimize the code → Do things like inling the functions
        4. It reduces the size of the application
        5. It removes the unused classes and method that contribute to the 64k method counts limit of an Android Application.
        6. It makes the application difficult to reverse engineer by obfuscating the code.
    - How it is useful for out application?
        - It's very useful for making a production-ready application.
        - It helps us to reduce the code and make apps faster.
        - It obfuscates the code, which means that it changes the names to some smaller names like for **MainViewModel** it might change the name to **A**. Reverse Engineering of your app becomes a tough task now after obfuscating the app.
        - It shrinks the resources i.e. ignorers the resources that are not called by our Class files, not being used in our android app like images from drawables, etc. This will reduce the app size by a lot. You should always shrink your app to keep it light weighted and fast.
        
    - How to use it in our Project?
        - To enable Proguard in your project, in the app's build.gradle add,
        
        ```kotlin
        buildTypes {
            release {
                minifyEnabledtrue
                proguardFilesgetDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        
            }
        }
        ```
        
        - Here, we have **`minfyEnabled`** as true, it activates the proguard which take from the file,
        
        ```kotlin
        proguard-android.txt
        ```
        
        - It is under the release block, which means that it will only be applied to the release of the build we generate.
        - `Issue:-`But it can be too much sometimes when the proguard removes too much code and it might break your code for the flow.So, configuring the code we have to add some custom rules to make sure we remove the set of code from obfuscating. We can fix this by writing out custom rules in our proguard and it will respect while generating the build.
        - Keeping Class Files
            
            Let say we have a data class, which is needed by some API to perform but which generating a build we obfuscate the class. For example, we have a User data class,
            
            ```kotlin
            data classUser(val id: String = "")
            ```
            
            and we want not to obfuscate the class which generating build then to ignore it from obfuscating we use **`@Keep`** annotation and update the code like,
            
            ```kotlin
            @Keepdata classUser(val id: String = "")
            ```
            
            This annotation helps the class to be ignored by using proguard while minified. This will preserve the class and its member functions even when they are not in use.
            
            We can also use,
            
            ```kotlin
            -keep
            ```
            
            to preserve options of class while generating the build. Using **-keep** over **@Keep** we get more control over what to preserve and what not to.
            
            But, we can also preserve the key of the **id** field in data model class by using @SerializedName (when using Gson library) like,
            
            ```kotlin
            data classUser(@SerializedName("id")
                             val id: String = "")
            ```
            
            If you notice here, we are not using @Keep.
            
        - Keeping the members for a class
            
            Let's say we want to preserve only the class members and not the class while shrinking, then we use,
            
            ```kotlin
            -keepclassmembers
            ```
            
            in the proguard rule file. This will help us to ignore members of a specific class.
            
            Consider the above User class, and we want to preserve all the public methods inside it. We write the rule like,
            
            ```kotlin
            -keepclassmembersclasscom.mindorks.sample.User{
            	public *;
            }
            ```
            
            Here, the class User keeps all the members all which have public modifiers.
            
        - Keeping names of the Class and members
            
            Let's say we want to keep all the same names of the class and members of a class if it's being used in the code i.e. if the class is not used it would be shrunk by proguard but not obfuscated because it has already been shrunk there is no need of obfuscation.
            
            To do the above task we use,
            
            ```kotlin
            -keepnames
            ```
            
            Practical use of it looks like,
            
            ```kotlin
            -keepnamesclasscom.mindorks.sample.GlideModule
            ```
            
            Here, if the GlideModule would keep all of its names of the class and the member function.
            
        - **Using any Library in Android**
            
            When using any library we might want to write some custom rules for proguard. There might a case when the library throws a warning in the logcat or they might not even have their own proguard rules!!!
            
            To fix that we need to add custom rules at our application side. For example, if we start getting warnings from any library then we add,
            
            ```
            -dontwarn com.somelibrary.annotations.*
            ```
            
            in our proguard rules and then we won't see any warning coming up in our logs.
            
            And to write custom rules for the library you can write it like any other rule for your own class.
            
        - **Only Obfuscate your project**
            
            Consider a very rare use case, where you just want to obfuscate the code and not shrink any resource. This is a very rare use case but might be useful for some small libraries, then we write the flags like,
            
            ```
            -dontshrink
            -dontoptimize
            ```
            
            This will help us to not shrink and optimize the code and just obfuscate.
            
        - **Maintaining annotations**
            
            While building the app, ProGuard removes all the annotation and it might still work fine for some set of codes in your project. But let's say if we need the annotations to not be removed then we have the option like,
            
            ```
            -keepattributes *Annotation*
            ```
            
            Here, it keeps the attributes for all annotations to be preserved in your app. It is by default present in our rules.
            
        - **Optimization**
            
            After writing this amount of rules in ProGuard, we might need to provide an extra layer of optimization for our app. First, we update the **build.gradle** file like,
            
            ```kotlin
            android {
              buildTypes {
                release {
                  proguardFilesgetDefaultProguardFile('proguard-android-optimize.txt')
                }
              }
            }
            ```
            
            Now, generally, we don't use this option but the use case here is we have to perform an extra level of optimizations.
            
            To increase the number of cycles in optimization for example like we want to check if the optimization is done properly or not and if it's not done it will optimize it again till a certain number of times we use,
            
            ```kotlin
            -optimizationpasses 5
            ```
            
            Here, it will run the optimization upto 5 times to make it more optimized.
            
            Now, consider an example where we want to optimize our final classes more at a granular level compared to what it was before, we use,
            
            ```kotlin
            -optimizationsclass/marking/final
            ```
            
            Here, the final classes will be optimized upto 5 times max or it might even end early if the optimization is already done.
            
            Now, if we want to optimize the private fields now we use,
            
            ```kotlin
            -optimizations field/marking/private
            ```
            
            The majority of times the optimization is done for the first time.
            
            If we don't want to optimize at all we use,
            
            ```kotlin
            -dontoptimize
            ```
            
            This is how we can work in different ways to make our app more secure and lighter using proguard.
            
        - **Important things to Note:**
            - Do not use something like *MainFragment.class.getSimpleName()* as a fragment TAG. Proguard may assign the same name (A.class) to two different fragments in different packages while obfuscating. In this case, two fragments will have the same TAG. It will lead to the bug in your application.
            - Keep your mapping file of the Proguard to trace back to the original code. You may have to upload it at different places like PlayStore Console for seeing the original stack-trace of the crashes.
- How to reduce APK size in Android
    - Remove Unused Resources
        - To reduce apk size is to remove unused resources in the application.
        - Use scalable drawable objects ( importing vector assets) instead of other image format like PNG, JPEG etc.
        - Using Vector Drawable is one of the best ways to reduce the size significantly.
    - Using Lint
        
        helps in generating warnings or unused code inside the application.
        
    - Reduse Libraries Size
        
        Check if you can reduce the size when it comes to the usage of libraries. For example, use only specific libraries of Google Play Services. Compile only which is required.
        
    - Reuse Code
        
        Object-Oriented Programming has solved a lot of problems in the programming world. Try reusing the code as much as possible instead of repetitive code. Repetitive code also leads to increased file size thereby effecting the Apk size.
        
    - Compressed PNG and JPEG files
        
        If using PNG and JPEG files is something mandatory in your project, you can compress them using image quality tools like TinyPNG.
        
    - Use WebP file format
        
        If you want to use the image whose file format is PNG then it is recommended to change the file to a WebP file format.
        
    - Use Proguard
        
        Every time we build a new project, we see the following piece of code in the app-level build.gradle file
        
        ```kotlin
        buildTypes {
            release {
                minifyEnabledfalse
                proguardFilesgetDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
            }
        }
        ```
        
        ProGuard makes the following impact on our project,
        
        - It reduces the size of the application.
        - It removes the unused classes and methods that contribute to the 64K method counts limit of an Android application.
        - It makes the application difficult to reverse engineer by obfuscating the code.
    - ShrinkResources
        - Reduce resources where ever possible.
        - Using ***shrinkResources*** attribute in the Gradle will remove all the resources which are not being used anywhere in the project.
        - Enable this in your app-level build.gradle file by adding below line:
        
        ```kotlin
        buildTypes {
            release {
                ........
                shrinkResourcestrue
                ........
            }
        }
        ```
        
    - DebugImplementation
        
        Remove any debug library you have in the app. It can be done by using ***debugImplementation*** while building testing debug apk.
        
    - Use R8 to reduce APK size
        - R8 shrinking is a process in which we reduce the amount of code of our application and by doing so, the APK size automatically gets reduced.
        - R8 does most of the work as Proguard.
        
        **Why do we need to prefer it?** 
        
        - The reason is it works with Proguard rules and shrinks the code faster while improving the output size.
- Understading Image Compression in Android
    
    I havn't covered this so if you are intrested to read it Link refer this [link](https://blog.mindorks.com/understanding-image-compression-in-android)
    
- Understading Image Compression in Android
    
    I havn't covered this so if you are intrested to read it Link refer this [link](https://blog.mindorks.com/understanding-image-compression-in-android)
    
- Difference between setValue() and postValue()
    - SetValue() → Sets the value. If there are active observers, the value will be dispatched to them. This method must be called from the main thread.
    - PostValue() →
- **[I want to build one feature in my app where a user performs a long press on a contact it will show option like make Call and send SMS. How we can do that.](https://www.knowledgehut.com/interview-questions/android#collapse-beginner-3470)sav**
    
    In android application when user long press on any content it will show an option to perform action this can be done using Context Menu. In your scenario, if user long presses on any contact we can show him a context menu with two options “MakeCall” and “Send SMS”. Please find below code for check how to implement a Context menu in our application:
    
    For adding context menu in our application we need register View who is going to display data at a long press on it. We will create registerForContextMenu(View) for register view in our activity and we need to override onCreateContextMenu() in our activity for displaying option to a user when the view has been long press by the user. In our scenario, Listview is having a list of contact so we will register Listview here. When user long press on any contact it call onCreateContaxtMenu method and show option like MakeCall and SendSMS. Please find below code for more detail:
    
    ```
    Listview listview  = (ListView) findViewById(R.id.listShow);
        registerForContextMenu(listview);
    }
    @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        super.onCreateContextMenu(menu, v, menuInfo);
        menu.setHeaderTitle("Context Menu");
        menu.add(0, v.getId(), 0, "Make Call");
        menu.add(0, v.getId(), 0, "Send SMS");
    ```
    
- What are the different software components of Android Jetpack?
    
    The software components of Android Jetpack has been divided into 4 categories:
    
    - **Foundation Components:** AppCompat, Android KTX, Test, Multidex
    - **Architecture Components:** Room, WorkManager, Lifecycle, ViewModel, Paging, Navigation
    - **Behavior Components:** DownloadManager, Permissions, Sharing, Slices
    - **UI Components:** Animation & Transition, Auto, Fragment, Palette, Layout
- What’s Retrofit in Android?
    
    Retrofit is a type-safe REST client build by square for Android and Java which intends to make it simpler to expand RESTful web services. Retrofit uses OkHttp as the system’s administration layer and is based on it. Retrofit naturally serializes the JSON reaction utilizing a POJO (PlainOldJavaObject) which must be characterized in cutting edge for the JSON Structure. To serialize JSON we require a converter to change over it into Gson first. Retrofit is much simpler than other libraries we don’t have to parse our JSON it directly returns objects but there is one disadvantage also it doesn’t provide support to load images from the server, but we can use Picasso for the same.
    
    so Basically it used to call the api website and convert the result into the POJO class through Seralizable 
    
- Camera
    - Writing Camera apps is Hard
        1. Difficult to master Camera2 API
        2. Inconsistency across devices
        3. Difficult to scale on-device testing (as cannot testit in every device it’s costly and time consuming).
    - Camerx makes it easy
        - Easier to implement
            - use case based approach
                - Preview → used to display the camera preview
                - ImageCapture → it’s for high quality still image for capture
                - ImageAnalysis → it’s for fame buffer across for analysis like object detection
            - PreviewView → to handle the complexity of the preview transfrom for you.
        - Consistent behavior across 94% of Android devices starting from API 21
        - Google conducts 24/7 on-device testing across a range of devices & API
- Alarm Manager
- How does Room Works Internally ?
    - Advantages of Using Room
        1. Compile-time verification of queries
        2. Reduces boilerplate code.
        3. Easy to understand and use.
        4. Easy integration with RxJava, LiveData and Kotlin Coroutines.
    - Components of Room
        1. Database → Contains the database holder and serves as the main access point for the underlying connection to your app’s persisted, relational data.
        2. Entity → Represents a table within the database.
        3. Dao → Contains the methods used for accessing the database.
    - Working
        
        Your application uses the **Room database** to get the **data access objects**, or **DAOs**, associated with your **database**. The app then uses each **DAO** to get **entities** from the **database** and save any changes to those **entities** back to the **database**. Finally, the app uses an **entity** to get and set values that correspond to table columns within the **database**.
        
    - Annotations
        1. @Database → 
- What is ADB?
    
    Android Debug Bridge is a command-line tool used to allow and control communication with an emulator instance. It gives the power for developers to execute remote shell commands to run applications on an emulator
    
- What is AIDL ? Which data types are supported by AIDL?
    
    AIDL(Android Interface Definition Language) is a tool that handles the interface requirements between a client and a service for interprocess communication(IPC) to communicate at the same level.
    
    The process involves dividing an object into primitives that are understood by the Android operating system. Data Types supported by AIDL is as follows:
    
    - String
    - List
    - Map
    - CharSequence
    - Java data types (int, long, char, and boolean)
- Provide some tips to reduce battery usage in an android application?
    - **Reduce network calls** as much as you can: Cache your data and retrieve it from the cache when required next time.
    - **Avoid wake lock as much as possible**: A wake lock is a mechanism to indicate that your application needs to have the device stay on.
    - **Use AlarmManager carefully**: Wrong use of AlarmManager can easily drain the battery.
    - **Batch the network calls**: You should batch the network calls if possible so that you can prevent the device from waking every second.
    - **A Different logic for Mobile Data and Wifi**: You should write different logic for mobile data and wifi as one logic may be optimized for mobile data and other may be optimized for wifi.
    - **Check all background processes**: You should check all the background processes.
    - **Use GPS carefully**: Do not use it frequently, use it only when actually required.
    - **Use JobScheduler**: This is an API for scheduling various types of jobs against the framework that will be executed in your application’s own process. The framework will be intelligent about when you receive your callbacks and attempt to batch and defer them as much as possible.
- Explain the build Process in Android?
    1. First step involves compiling the resources folder (/res) using the aapt (android asset packaging tool) tool. These are compiled to a single class file called R.java. This is a class that just contains constants.
    2. Second step involves the java source code being compiled to .class files by javac, and then the class files are converted to Dalvik bytecode by the “dx” tool, which is included in the sdk ‘tools’. The output is classes.dex.
    3. The final step involves the android apkbuilder which takes all the input and builds the apk (android packaging key) file.
- How to persist data in an Android app?
    1. Shared Preferences - to save primitive data in key-value pairs
    2. Internal Storage - you need to store data to the device filesystem, but you do not want any other app (even the user) to read this data
    3. External Storage - you might want the user to view the files and data saved by your app
    4. SQLite database
- What is Dalvik?
    - Dalvik is a Just in Time Compiler **(JIT)**
    - By the term JIT, we mean to say that whenever you run your app in your mobile device then that part of your code that is needed for execution of your app will only be compiled at that moment and rest of the code will be compiled in the future when needed.
    - The JIT or Just In Time compiles only a part of your code and it has a smaller memory footprint and due to this, it uses very less physical space on your device.
- What is vector?
    - Vector is a wrapper over an array, where in the array can grow in size, or reduce in size dynamically, without the developer having to manage the size.
    - Vector is synchronized, so it is a thread safe construct to use.
- Difference betweeen lateinit and lazy?
    - **lateinit property**
        
        lateinit properties are the var properties that can be initialised later in the constructor or in any function acording to the use.
        
        ```kotlin
        data class User (val id : Long,
                         val username : String) : Serializable
        
        lateinit var lateinitUser : User
        ```
        
    - **lazy property**
        
        lazy properties are the val properties that can also be initialised later when they are called the first time.
        
        ```kotlin
        val lazyUser : User? bylazy {
                User(id = 1, username = "agrawalsuneet")
            }
        ```
        
    - **lateinit var whereas lazy val**
        
        lateinit can only be used with a var property whereas lazy will always be used with val property. A lateinit property can be reinitialised again and again as per the use whereas the lazy property can only be initialised once.
        
        ```kotlin
        lateinitvar lateinitUser : User
        
        val lazyUser : User? by lazy {
                User(id = 1, username = "agrawalsuneet")
            }
        ```
        
    - **lateinit can't have custom getter or setter whereas lazy has custom getter**
        
        A lateinit property can't have a custom getter whereas a lazy property has a block that gets executed whenever the first time that property is called.
        
        ```kotlin
        
        val lazyUser : User bylazy {
                //can do other initialisation here
                User(id = 1, username = "agrawalsuneet")
            }
        
        ```
        
    - **isInitialized**
        
        In order to check if a lateinit property is initialised or not, we can use the extension function to KProperty directly which returns a boolean if the property is initialised or not.
        
        ```kotlin
        
        /**
         * Returns `true` if this lateinit property has been assigned a value, and `false` otherwise.
         *
         * Cannot be used in an inline function, to avoid binary compatibility issues.
         */
        @SinceKotlin("1.2")
        @InlineOnly
        inline val @receiver:AccessibleLateinitPropertyLiteral KProperty0<*>.isInitialized: Boolean
            get() = throw NotImplementedError("Implementation is intrinsic")
        
        println(::lateinitUser.isInitialized)
        
        ```
        
        Since the lazy block returns an object which implements the Lazy interface, we can check if the variable is initialised or not in the case of the lazy property also but for that, we need to split the lazy call.
        
        ```kotlin
        
        val lazyUserDelegate = lazy { User(id = 1, username = "agrawalsuneet") }
        val lazyUser by lazyUserDelegate
        
        println(lazyUserDelegate.isInitialized())
        
        ```
        
    - **Primitive types**
        
        lateinit properties can't be of primitive data types whereas lazy properties can be of primitive date types also.
        
        ```kotlin
        
        lateinit var lateinitInt : Int //compilation error: 'lateinit' modifier is not allowed on properties of primitive types
        
        val lazyInt by lazy {
            10
        }
        ```
        
    - **Thread Safety**
        
        We can't define the thready safety in case of lateinit property but in case of lazy, we can choose between SYNCHRONIZED, PUBLICATION and NONE.
        
        ```kotlin
        
        val lazyUser : User? by lazy(LazyThreadSafetyMode.SYNCHRONIZED) {
                User(id = 1, username = "agrawalsuneet")
            }
        ```
        
    - **Nullable Type**
        
        A lazy property can be of nullable type but a lateinit property can't be of nullable type.
        
        ```kotlin
        lateinit var lateinitUser : User? //compilation error: 'lateinit' modifier is not allowed on properties of nullable types
        
        val lazyUser : User? by lazy {
                User(id = 1, username = "agrawalsuneet")
            }
        ```
        
- Doze Mode?
    
    Doze mode is basically a state that intends to extend battery life by deferring app background CPU and network activity when a device is in an idle state for a long period of time. Here we have a maintenance window during which apps can complete pending works.
    
- What is the difference between FLAG_ACTIVITY_CLEAR_TASK and FLAG_ACTIVITY_CLEAR_TOP?
    - **FLAG_ACTIVITY_CLEAR_TASK** is used to clear all the activities from the task including any existing instances of the class invoked. The Activity launched by intent becomes the new root of the otherwise empty task list. This flag has to be used in conjunction with FLAG_ ACTIVITY_NEW_TASK.
    - **FLAG_ACTIVITY_CLEAR_TOP** on the other hand, if set and if an old instance of this Activity exists in the task list then barring that all the other activities are removed and that old activity becomes the root of the task list. Else if there’s no instance of that activity then a new instance of it is made the root of the task list. Using FLAG_ACTIVITY_NEW_TASK in conjunction is a good practice, though not necessary.
- Difference between Service, Intent Service, AsyncTask & Threads
    - **Android service** is a component that is used to perform operations on the background such as playing music. It doesn’t has any UI (user interface). The service runs in the background indefinitely even if application is destroyed.
    - **AsyncTask** allows you to perform asynchronous work on your user interface. It performs the blocking operations in a worker thread and then publishes the results on the UI thread, without requiring you to handle threads and/or handlers yourself.
    - **IntentService** is a base class for Services that handle asynchronous requests (expressed as Intents) on demand. Clients send requests through startService(Intent) calls; the service is started as needed, handles each Intent in turn using a worker thread, and stops itself when it runs out of work.
    - A **thread** is a single sequential flow of control within a program. Threads can be thought of as mini-processes running within a main process.
- Fragment & Activity Difference?
- Exception
    - An exception is an unexpected event, which occurs during the exception of a program i.e run time, that disrupts the normal flow of the program’s instruction.
    - **How JVM Handles the Exceptions?**
        
        Whenever inside a method, if an exception has occurred, the method creates an Object known as Exception Object and hands it off to the run-time system(JVM). The exception object contains name and description of the exception, and current state of the program where exception has occurred. Creating the Exception Object and handling it to the run-time system is called throwing an Exception.There might be the list of the methods that had been called to get to the method where exception was occurred. This ordered list of the methods is called **Call Stack**.Now the following procedure will happen.
        
        - The run-time system searches the call stack to find the method that contains block of code that can handle the occurred exception. The block of the code is called **Exception handler**.
        - The run-time system starts searching from the method in which exception occurred, proceeds through call stack in the reverse order in which methods were called.
        - If it finds appropriate handler then it passes the occurred exception to it. Appropriate handler means the type of the exception object thrown matches the type of the exception object it can handle.
        - If run-time system searches all the methods on call stack and couldn’t have found the appropriate handler then run-time system handover the Exception Object to **default exception handler** , which is part of run-time system. This handler prints the exception information in the following format and terminates program **abnormally**.
            
            ```java
            Exception in thread "xxx" Name of Exception : Description
            ... ...... ..  // Call Stack
            
            ```
            
        
        See the below diagram to understand the flow of the call stack.
        
        ![https://media.geeksforgeeks.org/wp-content/cdn-uploads/call-stack.png](https://media.geeksforgeeks.org/wp-content/cdn-uploads/call-stack.png)
        
- Difference Between Error and Exception?
    
    **Error:**
    
    An Error indicates serious problem that a reasonable application should not try to catch.
    
    **Exception:**
    
    Exception indicates conditions that a reasonable application might try to catch.
    
- What is the difference betweeen final, finally and finalize?
    - Final → It is an access modifier
    - Finally → is the block in the exception handing
    - Finalize → is the method of object class.
- Types of References in java?
    
    There are 4 types of references in Java
    
    - Strong Reference → It is the default type of reference object. An object that has active strong reference can’t be garbage collected. It is possible only if the variable that is strongly referenced points to null. Let us see an example −
    
    ## **Example**
    
    ```java
    class Demo {
       //Some functionality
    }
    public class Demo_example{
       public static void main(String[] args){
          Demo my_inst = new Demo();
          my_inst = null;
       }
    }
    ```
    
    - Weak Reference → They are not default class of reference object, hence need to be explicitly specified. It is generally used with WeakHashmap, so as to reference entry objects. Such weak references are marked for garbage collection by the Java Virtual Machine. Such references are created using the ‘java.lang.ref.WeakReference’ class.
    
    Let us see an example −
    
    ## **Example**
    
    [Live Demo](http://tpcg.io/7VS69hlE)
    
    ```
    import java.lang.ref.WeakReference;
    class Demo{
       public void display_msg(){
          System.out.println("Hello");
       }
    }
    public class Demo_sample{
       public static void main(String[] args){
          Demo inst = new Demo();
          inst.display_msg();
          WeakReference<Demo> my_weak_ref = new WeakReference<Demo>(inst);
          inst = null;
          inst = my_weak_ref.get();
          inst.display_msg();
    }
    ```
    
    ## **Output**
    
    ```
    Hello
    Hello
    ```
    
    A class named Demo has a function named ‘display_msg’. This function displays a relevant message. In another class named ‘Demo_sample’, the main function is defined, and an instance of Demo class is created. The ‘display_msg’ function is called on the instance. A weakReference to the Demo class is created, and the Demo insatne is assigned to null, and the function is called on it again. The relevant output is displayed on the console.
    
    ![https://www.tutorialspoint.com/assets/profiles/123055/profile/60_187394-1565938756.jpg](https://www.tutorialspoint.com/assets/profiles/123055/profile/60_187394-1565938756.jpg)    
    - Soft References
    - Phantom References
- Interface vs Abstract class?
