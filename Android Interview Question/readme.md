<h1 align="center">Interview Question For Android</h1>

- **Name the components of android?**
    
    App components are the essential building blocks of an Android app.
    
    Android Components:-
    
    - Activities:- An activity is the entry point for interacting with the user. It represents a single screen with a user interface. For example, an email app might have one activity that shows a list of new emails.
    
    - Services:- A Service is an application component that can perform long-running operations in the background. It does not provide a user interface. Once started, a service might continue running for some time, even after the user switches to another application
        
        ---
        
        A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons. It is a component that runs in the background to perform long-running operations or to perform work for remote processes. A service does not provide a user interface. For example, a service might play music in the background while the user is in a different app.
        
        Types :- Foregroud, Background, Bound
        
    
    - Broadcast receivers:-A broadcast receiver is a component that enables the system to deliver events to the app outside of a regular user flow, allowing the app to respond to system-wide broadcast announcements. Because broadcast receivers are another well-defined entry into the app, the system can deliver broadcasts even to apps that aren't currently running. A broadcast receiver is implemented as a subclass of BroadcastReceiver and each broadcast is delivered as an Intent object.
        
        ---
        
    
    Broadcast in android is the system-wide events that can occur when the device starts, when a message is received on the device or when incoming calls are received, or when a device goes to airplane mode, etc. Broadcast Receivers are used to respond to these system-wide events. Broadcast Receivers allow us to register for the system and application events, and when that event happens, then the register receivers get notified. There are mainly two types of Broadcast Receivers:
    
    - **Static Broadcast Receivers:** These types of Receivers are declared in the manifest file and works even if the app is closed.
    - **Dynamic Broadcast Receivers:** These types of receivers work only if the app is active or minimized.
    
    - Content providers:-A content provider manages a shared set of app data that you can store in the file system, in a SQLite database, on the web, or on any other persistent storage location that your app can access. Through the content provider, other apps can query or modify the data if the content provider allows it. For example, the Android system provides a content provider that manages the user's contact information. A content provider is implemented as a subclass of ContentProvider and must implement a standard set of APIs
- **What is the difference between commit and commitNow()?**
    
    **commit():**
    
    Schedules a commit of this transaction. The commit does not happen immediately; it will be scheduled as work on the main thread to be done the next time that thread is ready.
    
    If you are **performing multiple transactions**, **don’t need synchronicity**, or are **adding transactions to the back stack**, you should stick with commit().
    
    **commitNow():**
    
    If you need **synchronicity** and you are **not adding your transaction to the back stack**, use commitNow(). The support library uses this in Fragment PagerAdapter to guarantee that the correct pages have been added or removed at the end of an update. In general, it is fine to use this any time you are performing a transaction that you are not adding to the back stack.
    
- **What does commitAllowingStateLoss() method do?**
    
    Like commit() but allows the commit to be executed after an activity's state is saved. This is dangerous because the commit can be lost if the activity needs to later be restored from its state, so this should only be used for cases where it is okay for the UI state to change unexpectedly on the user.
    
- **How does the activity respond when the user rotates the screen?**
    
    Destroys current activity with  `onPause()` => `onStop()` => `onDestroy()`
    
    Creates same activity with different resources using  `onCreate()` => `onStart()` => `onResume()`
    
- **What are Launch Modes in Android?**
    
    Launch modes in Android help developers to launch Activities with a set of instructions on how it should associate with the task. By using the correct launch mode, you can achieve the required navigation behavior in a single line of code. To do so, you should first know the types of launch modes and how they work.
    
    **Standard**
    
    This is the default launch mode for Android `Activities`. It’ll create a new instance of the `Activity` every time in the target task.
    
    A common use case is to show the details of a component. For example, consider a movie application. Each time a user clicks on a movie item, we need to show the details of the movie in the `details` `Activity`.
    
    **SingleTop**
    
    If an instance of the `Activity` is already present in the task and it’s at the top of the task, then the Android OS will pass the intent data to the `onNewIntent` function of the `Activity` instead of creating a new instance.
    
    If there is no instance on the `Activity` in the task or the already existing instance of the task is not at the top of the task, then a new instance of the `Activity` will be created.
    
    **SingleTask**
    
    If the tasks don’t have an existing instance of the `Activity`, then a new instance is created that is similar to `singleTop`.
    
    If the tasks have an existing instance of the `Activity` and it’s at the top of the `Activity`, then the system will pass the intent data to the `onNewIntent` function.
    
    If the tasks have an existing instance but not at the top, then it’ll roll back to that `Activity` and destroy the `Activities` on top of the `SingleTask` `Activity`.
    
    **SingleInstance**
    
    When you invoke the `Activity` with `SingleInstance`, then the system will create a new special task that will only have one `SingleInstance` `Activity` in it. If you trigger any default `Activity` from the `SingleInstance` `Activity`, it’ll reroute to the previous task and create a new instance of the default `Activity`.
    
    If the instance of the `Activity` is already created, then the system will route to that task ****and use the `onNewIntent` function to pass the data.
    
- **onSavedInstanceState() and onRestoreInstanceState() in activity ?**
    - Before screen is rotated whatever whatever data we had we savedit using onSavedInstance function and after screen get rotated to get the same data we use onRestoreInstanceState.
- **How to prevent data from reloading and resetting when a screen is rotated?**
    
    The most basic approach would be to use a combination of ViewModels and onSaveInstanceState() . 
    
    So how we do we that?
    
    ☛ Basics of ViewModel: A ViewModel is LifeCycle-Aware. In other words, a ViewModel will not be destroyed if its owner is destroyed for a configuration change (e.g. rotation). The new instance of the owner will just re-connected to the existing ViewModel. So if you rotate an Activity three times, you have just created three different Activity instances, but you only have one ViewModel.
    
    ☛ So the common practice is to store data in the ViewModel class (since it persists data during configuration changes) and use OnSaveInstanceState to store small amounts of UI data.
    
    ☛ For instance, let's say we have a search screen and the user has entered a query in the Edittext. This results in a list of items being displayed in the RecyclerView. Now if the screen is rotated, the ideal way to prevent resetting of data would be to store the list of search items in the ViewModel and the query text user has entered in the OnSaveInstanceState method of the activity.
    
- **What are content providers? Example**
    
    A content provider component supplies data from one application to others on request. Such requests are handled by the methods of the ContentResolver class. A content provider can use different ways to store its data and the data can be stored in a database, in files, or even over a network.
    
    Content providers let you centralize content in one place and have many different applications access it as needed. A content provider behaves very much like a database where you can query it, edit its content, as well as add or delete content using insert(), update(), delete(), and query() methods. In most cases this data is stored in an **SQlite** database.
    
    A content provider is implemented as a subclass of **ContentProvider** class and must implement a standard set of APIs that enable other applications to perform transactions.
    
- **What are services and different types of services?**
    
    Services in Android are a special **component** that **facilitates an application to run in the background** in order to perform **long-running operation tasks.** The prime aim of a service is to ensure that the application remains active in the background so that the user can operate multiple applications at the same time. A user interface is not desirable for android services as it is designed to operate long-running processes without any user intervention. A service can run continuously in the background even if the application is closed or the user switches to another application. The service **does not have UI.**
    
    Type of Service:
    
    Foreground
    
    A foreground service performs some operation that is noticeable to the user. For example, an audio app would use a foreground service to play an audio track. Foreground services must display a [Notification](https://developer.android.com/guide/topics/ui/notifiers/notifications). Foreground services continue running even when the user isn't interacting with the app.
    When you use a foreground service, you must display a notification so that users are actively aware that the service is running. This notification cannot be dismissed unless the service is either stopped or removed from the foreground.
    
    Background
    
    A background service performs an operation that isn't directly noticed by the user. For example, if an app used a service to compact its storage, that would usually be a background service.
    
    Bound
    
    A service is *bound* when an application component binds to it by calling `[bindService()](https://developer.android.com/reference/android/content/Context#bindService(android.content.Intent,%20android.content.ServiceConnection,%20int))`. A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results, and even do so across processes with interprocess communication (IPC). A bound service runs only as long as another application component is bound to it. Multiple components can bind to the service at once, but when all of them unbind, the service is destroyed.
    
- **What are broadcast receivers?**
    
    Broadcast Receivers simply respond to broadcast messages from other applications or from the system itself. These messages are sometimes called events or intents. For example, applications can also initiate broadcasts to let other applications know that some data has been downloaded to the device and is available for them to use, so this is the broadcast receiver who will intercept this communication and will initiate appropriate action.
    
- **Different ways to communicate between service and activity/fragments?**
    1. Interface: The easiest way to communicate between your activity and fragments is using interfaces. The idea is basically to define an interface inside a given fragment A and let the activity implement that interface.
    2. ViewModel: The ViewModel case, makes things pretty simpler at the end, since you don't have to add extra logic that makes things dirty in the code and messy. Plus it will allow you to separate the gathering (through calls to an SQLite Database or an API) of data from the Controller (activities and fragments).
    3. call fragment method from the activity class.
    4. We can use Broadcast Sender and Receiver 
    5. we can use through Bundle also 
- **What is the difference when you extend a class with service and JobIntentService?**
    - Service - This runs on the same main thread which invokes this service and performs some background operation. For any long running operation happening on the main thread it is recommended to create a new thread and do the job (eg; `Handler`) by not impacting the main thread's performance.
        
        **Drawback: Runs on the main thread**
        
    - IntentService - Intent service also helps in doing some long-running (indefinite) background tasks. The only difference is that it creates a new thread to perform this task and does not run on the main thread. Does the given job on it's `onHandleIntent`.
        
        **Drawback: The job given to the IntentService would get lost when the application is killed**
        
    - JobIntentService - Job intent service is very similar to IntentService but with few benefits like the application can kill this job at any time and it can start the job from the beginning once the application gets recreated/up.
- **What is an AsyncTask?**
    
    AsyncTask is designed to be a helper class around `[Thread](https://developer.android.com/reference/java/lang/Thread)` and `[Handler](https://developer.android.com/reference/android/os/Handler)` and does not constitute a generic threading framework. AsyncTasks should ideally be used for short operations (a few seconds at the most.) If you need to keep threads running for long periods of time, it is highly recommended you use the various APIs provided by the `java.util.concurrent` package such as `[Executor](https://developer.android.com/reference/java/util/concurrent/Executor)`, `[ThreadPoolExecutor](https://developer.android.com/reference/java/util/concurrent/ThreadPoolExecutor)` and `[FutureTask](https://developer.android.com/reference/java/util/concurrent/FutureTask)`.
    
    An asynchronous task is defined by a computation that runs on a background thread and whose result is published on the UI thread. An asynchronous task is defined by 3 generic types, called `Params`, `Progress` and `Result`, and 4 steps, called `onPreExecute`, `doInBackground`, `onProgressUpdate` and `onPostExecute`.
    
    Android AsyncTask going to do background operation on background thread and update on main thread. In android we cant directly touch background thread to main thread in android development. asynctask help us to make communication between background thread to main thread.
    
- **What happens when an AsyncTask is running and inside the onPostExecute() method you are updating the textview but suddenly you rotate the screen**
    
    AsyncTask is a great thing to run complex tasks in another thread. When there is an orientation change or another configuration change while the AsyncTask is still running, the current Activity is destroyed and restarted. And as the instance of AsyncTask is connected to that activity, it fails and causes a "force close" message window.
    
- **What are handlers?**
    
    A Handler allows you to send and process `[Message](https://developer.android.com/reference/android/os/Message)` and Runnable objects associated with a thread's `[MessageQueue](https://developer.android.com/reference/android/os/MessageQueue)`. Each Handler instance is associated with a single thread and that thread's message queue. When you create a new Handler it is bound to a `[Looper](https://developer.android.com/reference/android/os/Looper)`. It will deliver messages and runnables to that Looper's message queue and execute them on that Looper's thread.
    
    There are two main uses for a Handler: 
    
    1.  To schedule messages and runnables to be executed at some point in the future; and (2) to enqueue an action to be performed on a different thread than your own.
    2. To enqueue an action to be performed on a different thread than your own. In other words enqueue an action to perform on different thread.
    
    How TO schedule ?
    
    Scheduling messages is accomplished with the post(Runnable), postAtTime(Runnable, long), postDelayed(Runnable, long), sendEmptyMessage(int), sendMessage(Message), sendMessageAtTime(Message, long), and sendMessageDelayed(Message, long) methods.
    
- **What are Loopers?**
    
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
    
- **What is a Message-Queue?**
    
    Low-level class holding the list of messages to be dispatched by a Looper. Messages are not added directly to a MessageQueue, but rather through Handler objects associated with the Looper. MessageQueue is a message loop or message queue which basically contains a list of Messages or Runnables (set of executable code).
    
- **Difference between Serializable and Parceable?**
    
    In Android, we cannot just pass objects to activities. To do this the objects must either implement `Serializable` or `Parcelable` interface.
    
    **Serializable**
    
    `Serializable` is a standard Java interface. You can just implement `Serializable` interface and add override methods. The problem with this approach is that reflection is used and it is a slow process. This method creates a lot of temporary objects and causes quite a bit of garbage collection. However, `Serializable` interface is easier to implement.
    
    Serializable is a standard Java interface. You simply mark a class Serializable by implementing the interface, and Java will automatically serialize it in certain situations.
    
    **Parcelable**
    
    `Parcelable` process is much faster than `Serializable`. One of the reasons for this is that we are being explicit about the serialization process instead of using reflection to infer it. It also stands to reason that the code has been heavily optimized for this purpose.
    
    Parcelable is an Android-specific interface where you implement the serialization yourself. It was created to be far more efficient than Serializable, and to get around some problems with the default Java serialization scheme.
    
    Parcelable is a better choice since it is recommended by Google.
    
- **How would you update the UI from the background thread?**
    
    
    Although using ‘onPostExecute’ in an ‘AsyncTask’ is one of the solutions, that cannot be applied everywhere, especially where there is no Async Task (eg. when you are making an asynchronous network call with the help of a third party library). Wrapping up a **synchronous** network call with **Async Task** is one of the ways of using the AsyncTask.
    
    I recently encountered the same problem when I wanted to make an **asynchronous** call using HttpOk library and then I came to know about this…
    
    [https://qphs.fs.quoracdn.net/main-qimg-a620f83f23dd32685988b07c1e15efb4](https://qphs.fs.quoracdn.net/main-qimg-a620f83f23dd32685988b07c1e15efb4)
    
    We make a new **runnable** in something called **runOnUiThread()**. Then, we tell the system to run particular lines of code on the UI thread. The syntax is shown above. Instead of MainActivity.class, the actual Activity name should be used, and in the run() function, you can mention the code you want to be executed in the UI thread.
    
    You can insert the above bit of code in the location where you want the actions to be performed on the main UI thread.
    
- **What is the intent? What is the maximum amount of data that you can transfer using intent?**
    
    Android Intent Tutorial. Android Intent is the message that is passed between components such as activities, content providers, broadcast receivers, services, etc.
    
    The maximum amount of data transfer is approx 1MB 
    
- **Types of intent? What is implicit intent? What is explicit intent?**
    
    There are two types of intent in Android. They are Implicit Intents and Explicit Intents.
    
    Now that we have seen Implicit Intent. Let us understand the other type of intent: Explicit Intent. (**this is done to shift within the activity**)
    
    The explicit intent is very different from the implicit as it requires a component. The developer must define the intent filters in the manifest. For the Android system to resolve the intent.
    
    A real world use case of explicit intent is starting an Activity. Example code:
    
    ```
    val intent = Intent(this, TargetedActivity::class.java)
    context.startActivity(intent)
    
    ```
    
    Implicit by its definition is something that is not definite. In other words the there is no one answer to how things will happen. (**this is done to shift from app to webpage** )
    
    And the implicit intent is something similar. The component is not known for an implicit intent. And there may be multiple available options at any given time.
    
    An example of such intent is opening an image picker, sharing data with other applications, receiving broadcasts, etc.
    
    There might be multiple components to handle such information. And the process involved is known as intent resolution. It is done with the help of **intent filters**.
    
    Look at the code below:
    
    ```
    val intent:Intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
    startActivity(intent)
    ```
    
- **What is a pending intent?**
    
    A PendingIntent is a token that you give to a foreign application (e.g. NotificationManager, AlarmManager, Home Screen AppWidgetManager, or other 3rd party applications), which allows the foreign application to use your application's permissions to execute a predefined piece of code.
    
- **What is an Intent Filter?**
    
    An intent filter is an instance of the IntentFilter class. Intent filters are helpful while using implicit intents, It is not going to handle in java code, we have to set it up in AndroidManifest.xml. Android must know what kind of intent it is launching so intent filters give the information to android about intent and actions.
    
    Before launching intent, android going to do action test, category test and data test. This example demonstrate about how to use intent filters in android.
    
    To more understated refer this link [https://www.tutorialspoint.com/what-are-intent-filters-in-android](https://www.tutorialspoint.com/what-are-intent-filters-in-android)
    
- **When should you use a fragment rather than an Activity?**
    
    Fragments are Android's solution to creating reusable user interfaces. You can achieve some of the same things using activities and layouts (for example by using includes). However; fragments are wired in to the Android API, from HoneyComb, and up. Let me elaborate;
    
    - The `ActionBar`. If you want tabs up there to navigate your app, you quickly see that `ActionBar.TabListener` interface gives you a `FragmentTransaction` as an input argument to the `onTabSelected` method. You could probably ignore this, and do something else and clever, but you'd be working against the API, not with it.
    - The `FragmentManager` handles «back» for you in a very clever way. Back does not mean back to the last activity, like for regular activities. It means back to the previous fragment state.
    - You can use the cool `ViewPager` with a `FragmentPagerAdapter` to create swipe interfaces. The `FragmentPagerAdapter` code is much cleaner than a regular adapter, and it controls instantiations of the individual fragments.
    - Your life will be a lot easier if you use Fragments when you try to create applications for both phones and tablets. Since the fragments are so tied in with the Honeycomb+ APIs, you will want to use them on phones as well to reuse code. That's where the compatibility library comes in handy.
    - You even could and should use fragments for apps meant for phones only. If you have portability in mind. I use `ActionBarSherlock` and the compatibility libraries to create "ICS looking" apps, that look the same all the way back to version 1.6. You get the latest features like the `ActionBar`, with tabs, overflow, split action bar, viewpager etc.
    
    > Bonus 2
    > 
    
    The best way to communicate between fragments are intents. When you press something in a Fragment you would typically call `StartActivity()` with data on it. The intent is passed on to all fragments of the activity you launch.
    
- **Why is it recommended to use a default constructor while creating a fragment?**
    - Android Frame Works decide to recreate our fragment
    - Orientation Changes
    - Android calls the no-argument function
    - it has no idea what constructor we have called
- **What is Context?**
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
    
    ***Types of Context :- Application Context and Activity Context***
    
- **What is Application Context?**
    - It is the application and we are present in Application. For example - MyApplication(which extends Application class). It is an instance of MyApplication only.
    - Both the Activity and Application classes extend the Context class.
    - It is an instance that is the singleton and can be accessed in activity via `getApplicationContext()`. This context is tied to the lifecycle of an application. The application context can be used where you need a context whose lifecycle is separate from the current context or when you are passing a context beyond the scope of activity.
    - Example Use: If you have to create a singleton object for your application and that object needs a context, always pass the application context.
    - If you pass the activity context here, it will lead to the memory leak as it will keep the reference to the activity and activity will not be garbage collected.
    - In case, when you have to initialize a library in an activity, always pass the application context, **not** **the activity context**.
    - You only use `getApplicationContext()` when you know you need a `Context` for something that may live longer than any other likely `Context` you have at your disposal.
    - Wrong use of Context can easily lead to memory leaks in an android application
- **What is Activity Context?**
    - This context is available in an activity. This context is tied to the lifecycle of an activity. The activity context should be used when you are passing the context in the scope of an activity or you need the context whose lifecycle is attached to the current context.
    - Example Use: If you have to create an object whose lifecycle is attached to an activity, you can use the activity context.
    
    The app hierarchy looks like the following:
    
    ![https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/context-app-activity-hierarchy.jpg](https://s3.ap-south-1.amazonaws.com/mindorks-server-uploads/context-app-activity-hierarchy.jpg)
    
    - MyApplication [Here we have only Application context present] [Nearest Context is Application Context]
    - MainActivity1 [Here we have both Activity(MainActivity1) context and Application context present] [Nearest Context is Activity Context]
    - MainActivity2 [Here we have both Activity(MainActivity2) context and Application context present] [Nearest Context is Activity Context]
    - It returns the Context which is linked to the Activity from which it is called. This is useful when we want to call the context from only the current running activity. and it can be used for toast, intent start activity
- **When to use Context and Application context?**
    
    Let's learn which context to use at which place with an example:
    
    - Suppose we have our class MyApplication(which extends the Application class). And, another class MyDB which is Singleton. And MyDB(which is Singleton) needs context. Which context will we be passing?
    - The answer is Application Context because if we pass the Activity Context (for example MainActivity1), even if MainActivity1 is not in use, the MyDB will be keeping the reference unnecessary which will lead to the memory leaks.
    - So always remember, in case of Singleton(lifecycle is attached to the application lifecycle), always use the Application Context.
    - So, now when to use the Activity Context. Whenever you are in Activity, for any UI operations like showing toast, dialogs, and etc, use the Activity Context.
    - Always try to use the nearest context which is available to you. When you are in Activity, the nearest context is Activity context. When you are in Application, the nearest context is the Application context. If Singleton, use the Application Context
- **When to not to use Application context?**
    - It’s not a complete `Context`, supporting everything that `Activity` does. Various things you will try to do with this `Context` will fail, mostly related to the GUI.
    - It can create memory leaks if the `Context` from `getApplicationContext()` holds onto something created by your calls on it that you don’t clean up. With an `Activity`, if it holds onto something, once the `Activity` gets garbage collected, everything else flushes out too. The `Application` object remains for the lifetime of your process.
- **What is setRetainInstance(true) in fragments ?**
- **What is the difference between padding and margin?**
    
    [Margin vs Padding](https://www.notion.so/0c82360fe6954eada5d4b5f2b7f350b4)
    
- **What is the difference between a ViewGroup and View?**
    - *ViewGroup → will provide an invisible container to hold other Views or ViewGroups and to define the layout properties. For example, Linear Layout is the ViewGroup that contains UI controls like Button, TextView, etc., and other layouts also.*
    - *ViewGroup → Refer to the android.view.ViewGroup class, which is the base class of some special UI classes that can contain other View objects as children.*
    - *The View class is the base class or we can say that it is the superclass for all the GUI components in android. For example, the EditText class is used to accept the input from users in android apps, which is a subclass of View*
    
    ---
    
    - **Additional** (View is a basic building block of UI (User Interface) in android. A view is a small rectangular box that responds to user inputs. Eg: EditText, Button, CheckBox, etc. ViewGroup is an invisible container of other views (child views) and other ViewGroup. Eg: LinearLayout is a ViewGroup that can contain other views in it. ViewGroup is a special kind of view that is extended from View as its base class. ViewGroup is the base class for layouts. As the name states View is singular and the group of Views is the ViewGroup)
- **What is the difference between a relative layout and Linear Layout?**
    - ***Linear layout*** displays its views continue one after one, either vertically or horizontally. You need to specify orientation to define whether layout is vertical or horizontal.
        1. **Weight:** It specifies how much space each view spans relative to others. For example, in an e-mail application, you can give less weight to ‘To’ and ‘Subject’, and more weight to ‘Message’.
        2. **Gravity:** It defines placement of a view’s contents.
        3. **Layout Gravity:** It defines the placement of the view itself.
    - ***What is Relative Layout and it’s property*** A relative layout displays its views relative to one another, so order is not that important. You can define the top most view at the end of the layout and provide details to show it on top left. Here are some points which will help you to understand about RelativeLayout.
        1. **Position relative to screen:** You can align a view relative to screen using alignParentTop, centerHorizontal etc.
        2. **Position relative to other views:** You can align a view relative to another view using above, below, toLeftOf etc.
        3. **Margins:** You can provide margins using marginTop, marginLeft etc.
- **How to support different screen sizes in Android?**
    - Use constraints Layout:- ConstraintLayout allows you to specify the position and size for each view according to spatial relationships with other views in the layout. This way, all the views can move and stretch together as the screen size changes.
    - Use SlidingPaneLayout for list/detail UIs
    - Avoid hard-coded layout sizes
    
    To ensure that your layout is flexible and adapts to different screen sizes, you should use `"wrap_content"` or `"match_parent"` for the width and height of most view components, instead of hard-coded sizes.
    
    `"wrap_content"` tells the view to set its size to whatever is necessary to fit the content within that view.
    
    `"match_parent"` makes the view expand to as much as possible within the parent view.
    
- **What is the lifecycle of a View?**
    
    # **View Life Cycle**
    
    Every Activity has it’s own life cycle similarly Views also have a Life Cycle. A view which was rendered on the screen must undergo these lifecycle methods to get drawn on the screen correctly. Each of these methods has its importance. Let’s dive into the life cycle.
    
    [https://miro.medium.com/max/875/0*cHmlPwPvhWJ15zU3](https://miro.medium.com/max/875/0*cHmlPwPvhWJ15zU3)
    
    ### **Constructors**
    
    Usually, we get confused about why there are four types of constructors for a View
    
    ```
    View(Context context) View(Context context, @Nullable AttributeSet attrs) View(Context context, @Nullable AttributeSet attrs, int defStyleAttr) View(Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes)
    ```
    
- **What is a custom view? What all methods do you override?**
    
    Android offers a sophisticated and powerful componentized model for building your UI, based on the fundamental layout classes: `[View](https://developer.android.com/reference/android/view/View)` and `[ViewGroup](https://developer.android.com/reference/android/view/ViewGroup)`. To start with, the platform includes a variety of prebuilt View and ViewGroup subclasses — called widgets and layouts, respectively — that you can use to construct your UI.
    
    A partial list of available widgets includes `[Button](https://developer.android.com/reference/android/widget/Button)`, `[TextView](https://developer.android.com/reference/android/widget/TextView)`, `[EditText](https://developer.android.com/reference/android/widget/EditText)`, `[ListView](https://developer.android.com/reference/android/widget/ListView)`, `[CheckBox](https://developer.android.com/reference/android/widget/CheckBox)`, `[RadioButton](https://developer.android.com/reference/android/widget/RadioButton)`, `[Gallery](https://developer.android.com/reference/android/widget/Gallery)`, `[Spinner](https://developer.android.com/reference/android/widget/Spinner)`, and the more special-purpose `[AutoCompleteTextView](https://developer.android.com/reference/android/widget/AutoCompleteTextView)`, `[ImageSwitcher](https://developer.android.com/reference/android/widget/ImageSwitcher)`, and `[TextSwitcher](https://developer.android.com/reference/android/widget/TextSwitcher)`.
    
    Among the layouts available are `[LinearLayout](https://developer.android.com/reference/android/widget/LinearLayout)`, `[FrameLayout](https://developer.android.com/reference/android/widget/FrameLayout)`, `[RelativeLayout](https://developer.android.com/reference/android/widget/RelativeLayout)`, and others. For more examples, see [Common Layout Objects](https://developer.android.com/guide/topics/ui/layout-objects).
    
    **Methods to override:**
    
    The superclass methods to override start with 'on', for example, onDraw(), onMeasure(), and onKeyDown().
    
- **What is an Application Not Responding dialogue? When it usually occurs?**
    
    When an **[app](https://techterms.com/definition/app)** is running on an Android device and stops responding, an "ANR" event is triggered. Two conditions may cause an ANR error on an Android device:
    
    1. An active app does not respond to an **[input](https://techterms.com/definition/input)** event within 5 seconds.
    2. The **BroadcastReceiver** **[class](https://techterms.com/definition/class)** does not finish executing after a long period of time.
    
    If an ANR error happens on your Android device, a **[dialog box](https://techterms.com/definition/dialogbox)** will appear on the screen. The message will inform you the application is not responding and will ask if you want to close the app. You have two options: Wait or OK. Choosing "Wait" will allow you to keep waiting if you want to give the app more time. Choosing "OK" will close the app and you may lose unsaved activity.
    
    ANRs are different than crashes. A **[crash](https://techterms.com/definition/crash)** causes a program to quit unexpectedly. An ANR causes a program to "hang" in an unresponsive state for a few seconds, but it may recover.
    
    ANR errors happen for many different reasons. Some are developer-related, such as a poorly written **[function](https://techterms.com/definition/function)** that loops more times than necessary. Others are device-related, meaning the hardware cannot keep up with the demands of the app. For example, if an app is rendering a large **[document](https://techterms.com/definition/document)**, it may take several seconds to load the data and **[render](https://techterms.com/definition/rendering)** the image on the screen. This could produce an ANR message, though the **[process](https://techterms.com/definition/process)** might complete a few seconds later.
    
- **What happens when you make an API request on the UI thread?**
    
    Network operations and database calls, as well as loading of certain components, are common examples of operations that one should avoid in the main thread. When they are called in the main thread, they are called synchronously, which means that the UI will remain completely unresponsive until the operation completes. For this reason, they are usually performed in separate threads, which thereby avoids blocking the UI while they are being performed (i.e., they are performed asynchronously from the UI).
    
    To keep your application responsive, it is essential to avoid using the main thread to perform any operation that may end up keeping it blocked.
    
- **What are the differences between Thread & Async tasks?**
    
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
- **What is a singleton class?**
    
    In object-oriented programming, a singleton class is a class that can have only one object (an instance of the class) at a time.
    
    After first time, if we try to instantiate the Singleton class, the new variable also points to the first instance created. So whatever modifications we do to any variable inside the class through any instance, it affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined.
    
    Let us brief how singleton class varies from normal class in java. Here the difference is in terms of instantiation as for normal class we use constructor, whereas for singleton class we use getInstance() method which we will be peeking out in the example 1 as depicted below. In general, in order to avoid confusion we may also use the class name as method name while defining this method which will be as depicted in the example 2 below as follows.
    
- **What is the difference between commit and apply in sharedpreferences?**
    
    the differences of commit() and apply().
    
    1. Return value:
    
    ```
    apply() commitswithout returning a boolean indicating success or failure.commit() returnstrue if the save works,false otherwise.
    ```
    
    2. Speed:
    
    ```
    apply() isfaster.commit() isslower.
    ```
    
    3. Asynchronous v.s. Synchronous:
    
    ```
    apply():Asynchronouscommit():Synchronous
    ```
    
    4. Atomic:
    
    ```
    apply(): atomiccommit(): atomic
    ```
    
    5. Error notification:
    
    ```
    apply():Nocommit():Yes
    ```
    
- **What is a recycler view and How does it work?**
    
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
    
    ### Android Online Course for Professionals by MindOrks
    
    Join and learn Dagger, Kotlin, RxJava, MVVM, Architecture Components, Coroutines, Unit Testing and much more.
    
    **[ENROLL NOW](https://mindorks.com/android-app-development-online-course-for-professionals)**
    
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
    
- **What is the difference between a Listview and RecyclerView?**
    1. **ViewHolder Pattern**
    
    In a ListView, it was recommended to use the ViewHolder pattern but it was never a compulsion. In case of RecyclerView, this is mandatory using the [RecyclerView.ViewHolder](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ViewHolder.html) class. This is one of the major differences between the ListView and the RecyclerView.
    
    It makes things a bit more complex in RecyclerView but a lot of problems that we faced in the ListView are solved efficiently.
    
    **2. LayoutManager**
    
    This is another massive enhancement brought to the RecyclerView. In a ListView, the only type of view available is the vertical ListView. There is no official way to even implement a horizontal ListView.
    
    Now using a RecyclerView, we can have a
    
    i) [LinearLayoutManager](https://developer.android.com/reference/android/support/v7/widget/LinearLayoutManager.html) — which supports both vertical and horizontal lists,
    
    ii) [StaggeredLayoutManager](https://developer.android.com/reference/android/support/v7/widget/StaggeredGridLayoutManager.html) — which supports Pinterest like staggered lists,
    
    iii) [GridLayoutManager](https://developer.android.com/reference/android/support/v7/widget/GridLayoutManager.html) — which supports displaying grids as seen in Gallery apps.
    
    And the best thing is that we can do all these dynamically as we want.
    
    **3. Item Animator**
    
    ListViews are lacking in support of good animations, but the RecyclerView brings a whole new dimension to it. Using the [RecyclerView.ItemAnimator](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ItemAnimator.html) class, animating the views becomes so much easy and intuitive.
    
    **4. Item Decoration**
    
    In case of ListViews, dynamically decorating items like adding borders or dividers was never easy. But in case of RecyclerView, the [RecyclerView.ItemDecorator](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ItemDecoration.html) class gives huge control to the developers but makes things a bit more time consuming and complex.
    
    **5. OnItemTouchListener**
    
    Intercepting item clicks on a ListView was simple, thanks to its [AdapterView.OnItemClickListener](http://developer.android.com/reference/android/widget/AdapterView.OnItemClickListener.html) interface. But the RecyclerView gives much more power and control to its developers by the [RecyclerView.OnItemTouchListener](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.OnItemTouchListener.html) but it complicates things a bit for the developer.
    
    In simple words, the RecyclerView is much more customizable than the ListView and gives a lot of control and power to its developers.
    
    **6. Performance on Loading**
    
    RecyclerView prepares view just ahead and behind the visible entries, which is great if you are fetching bitmaps in background. Performance is dramatically faster, especially if you use RecyclerView.setHasFixedSize. The old ListView is based on the premise that there’s no way to precalculate or cache the size of entries in the list, which causes insane complications when scrolling and performing layout. Takes a while to get used to it, but once you do, you’ll never go back
    
- **Tell me the different ways to optimize the app size?**
    
    [https://developer.android.com/topic/performance/reduce-apk-size](https://developer.android.com/topic/performance/reduce-apk-size)
    
- **What is this keyword?**
    
    The `this` keyword refers to the current object in a method or constructor.
    
    The most common use of the `this` keyword is to eliminate the confusion between class attributes and parameters with the same name (because a class attribute is shadowed by a method or constructor parameter). If you omit the keyword in the example above, the output would be "0" instead of "5".
    
    `this` can also be used to:
    
    - Invoke current class constructor
    - Invoke current class method
    - Return the current class object
    - Pass an argument in the method call
    - Pass an argument in the constructor call
- **What is super()?**
    
    The super keyword in Java is a reference variable which is used to refer immediate parent class object.
    Whenever you create the instance of subclass, an instance of parent class is created implicitly which is
    referred by super reference variable.
    Usage of Java super Keyword
    1. super can be used to refer immediate parent class instance variable.
    2. super can be used to invoke immediate parent class method.
    3. super() can be used to invoke immediate parent class constructor.
    
- **There are 2 threads T1 and T2, how would you ensure that the thread T2 will complete after T1?**
- **What is the yield method in thread class?**
    
    A yield() method is a static method of Thread class and it can stop the currently executing thread and will give a chance to other waiting threads of the same priority. If in case there are no waiting threads or if all the waiting threads have low priority then the same thread will continue its execution. The advantage of yield() method is to get a chance to execute other waiting threads so if our current thread takes more time to execute and allocate processor to other threads.
    
- **What is a static variable? What is the difference between a normal and a static variable?**
    
    **Static Variable**
    
    A static variable is also called a class variable and is common across the objects of the class and this variable can be accessed using class name as well.
    
    **Non-Static Variable**
    
    Any variable of a class which is not static is called non-static variable or an instance variable.
    
    Following are the important differences between static and non-static variable.
    
    [Untitled](https://www.notion.so/5bd929554ceb4c929cbf159a6e4c6b00)
    
- **Explain 4 OOPs principles ( with practical examples)**
    
    [OOPS Concepts](https://www.notion.so/OOPS-Concepts-388764da9639474e8e6fb5d19d464bce)
    
- **What is the difference between an Array and an ArrayList and mutable list?**
- **How is ArrayList implemented internally?**
- **How does a HashSet avoid duplicate elements? How does it work internally?**
- **What is the difference between Thread.run() and Thread.start() ?**
- **Can you override static methods?**
- **Can you overload static methods?**
- **Can an interface extend one more interface?**
- **How HashMap works internally?**
- **What is the difference between a comparator and comparable ?**
- **What is the difference between the below 2 string object creation?**
    
    **String a = “Abc”;**
    
    **String b = new String(“Abc”);**
    
- **What is a string pool?**
- **What is the finalize() method in Object class?**
    
    The finalize() method of Object class is a method that the Garbage Collector always calls just before the deletion/destroying the object which is eligible for Garbage Collection, so as to perform clean-up activity. Clean-up activity means closing the resources associated with that object like Database Connection, Network Connection or we can say resource de-allocation. Remember it is not a reserved keyword. Once the finalize method completes immediately Garbage Collector destroy that object.
    
- **What is the difference between StringBuffer and StringBuilder?**
    
    Java provides three classes to represent a sequence of characters: String, StringBuffer, and StringBuilder. The String class is an immutable class whereas StringBuffer and StringBuilder classes are mutable.
    
    [StringBuffer and StringBuilder](https://www.notion.so/03eae80dc8b54456b6b26c02b5a02c6a)
    
- **What are immutable classes? How can you make a class immutable?**
    
    An object is immutable if its state cannot change after construction. Immutable objects don’t expose any way for other objects to modify their state; the object’s fields are initialized only once inside the constructor and never change again.
    
    In this article, we'll define the typical steps for creating an immutable class in Java and also shed light on the common mistakes which are made by developers while creating immutable classes.
    
    In order to create an immutable class, you should follow the below steps:
    
    1. **Make your class *final,*** so that no other classes can extend it.
    2. **Make all your fields *final,*** so that they’re initialized only once inside the constructor and never modified afterward.
    3. **Don’t expose setter methods.**
    4. When exposing methods that modify the state of the class, you must always return a new instance of the class.
    5. If the class holds a mutable object:
        - Inside the constructor, make sure to use a clone copy of the passed argument and never set your mutable field to the real instance passed through the constructor, this is to prevent the clients who pass the object from modifying it afterward.
        - Make sure to always return a clone copy of the field and never return the real object instance.
- **How many primitives are there in java?**
    
    There are 8 primitive types of data built into the Java language. These include: int, byte, short, long, float, double, boolean, and char.
    
- **What are exceptions?**
    
    In Java “an event that occurs during the execution of a program that disrupts the normal flow of instructions” is called an exception. This is generally an unexpected or unwanted event which can occur either at compile-time or run-time in application code.
    
    eg. null-pointer exception, can't  access member of UI thread on background thread
    
- **Difference between throw and throws?**
    - The throw and throws is the concept of exception handling where the throw keyword throw the exception explicitly from a method or a block of code whereas the throws keyword is used in signature of the method.
    - 
- **What is a finally block in try-catch?**
    
    A catch -block contains statements that specify what to do if an exception is thrown in the try -block. ... The finally -block will always execute after the try -block and catch -block(s) have finished executing. It always executes, regardless of whether an exception was thrown or caught. A finally block of code always executes, irrespective of occurrence of an Exception. Using a finally block allows you to run any cleanup-type statements that you want to execute, no matter what happens in the protected code.
    
- **Can a catch block exist without a try block?**
    
    We can't have catch or finally clause without a try statement. We can have multiple catch blocks with a single try statement. try-catch blocks can be nested similar to if-else statements. We can have only one finally block with a try-catch statement.
    
- **Can a finally block exist without a try block?**
    
    Finally cannot be used without a try block. The try block defines which lines of code will be followed by the finally code. If an exception is thrown prior to the try block, the finally code will not execute. The finally block always executes when the try block exits.
    
- **What is synchronization?**
    
    Synchronization in java is the capability to control the access of multiple threads to any shared resource. In the Multithreading concept, multiple threads try to access the shared resources at a time to produce inconsistent results. The synchronization is necessary for reliable communication between threads.
    
- **What is a singleton class?**
    
    singleton class is a class that can have only one object (an instance of the class) at a time.
    
    After first time, if we try to instantiate the Singleton class, the new variable also points to the first instance created. So whatever modifications we do to any variable inside the class through any instance, it affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined.
    
    1. Make constructor as private.
    2. Write a static method that has return type object of this singleton class. Here, the concept of **[Lazy initialization](https://en.wikipedia.org/wiki/Lazy_initialization)** is used to write this static method.
- **What is a builder pattern for creating objects?**
    
    The Builder is a creational pattern. With Builder pattern we can separate the construction of a complex object from its representation and build different objects using same construction process. Builder pattern is more likely implemented using method cascading.
    
    As mentioned in the Gang of four -
    
    *“Separate the construction of a complex object from its representation so that the same construction process can create different representations.”*
    
    **Where to use?**
    
    Following are the conditions which we can easily handle using builder design pattern-
    
    1. When multiple representation of objects are required.
    
    2. Too many argument to pass from client.
    
    3. Object creation contains optional parameter.
    
- **What is the parent class of all the classes?**
    - The Object class is the parent class of all the classes in java by default as it's the topmost class of java.
    - If a Class does not extend any other class then it is direct child class of Object and if extends other class then it is an indirectly derived. Therefore the Object class methods are available to all Java classes. Hence Object class acts as a root of inheritance hierarchy in any Java Program
    - lang. Object class is the super base class of all Java classes. Every other Java classes descends from Object
- **Difference between MutableLiveData and Live Data?**
    
    MLD - can change the data 
    
    LD - cant change the data 
    
- **what is a call?**
- **Difference between post value and set value?**
