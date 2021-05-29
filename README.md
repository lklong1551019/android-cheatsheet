# Android Cheatsheet

My cheatsheet which includes my experience working with Android development. This does not include the ones that are already mentioned at other sites.

You can also check for others's for more detail:\
    - https://github.com/MindorksOpenSource/android-interview-questions \
    - https://android.jlelse.eu/android-interview-questions-cheat-sheet-part-ii-bea0633f0da7
 
# Contents

* [Core Android](#core-android)
* [Java and Kotlin](#java-and-kotlin)
* [Tricky or unknown bugs](#tricky-or-unknown-bugs)
* [Solutions](#solutions)
* [AndroidX](#androidx)


### Core Android



#### Activity and Fragment

* **Some cases when activity's lifecycle transition to another** - [Learn from here](https://developer.android.com/guide/components/activities/state-changes)
     - Configuration change occurs, which can also triggered by language changing.
     - App enters multi-window mode and/or resized in this mode. Only the most recent activity that is interacted is in the `onResume()` state, the other is in `onPause()` state.
     - New activity/dialog appears in the foreground, taking focus and partialy/entirely cover the current activity. The current activity enters `onPause()/onResume()` respectively.

* **Activity launch modes** - [Learn from here](https://developer.android.com/guide/components/activities/tasks-and-back-stack)
     - SingleTop: If backstack contains A-B:
        - A new intent arrives for B, B is singleTop: B receives `onNewIntent()`. Backstack is now A-B.
        - A new intent arrives for A, A is singleTop: create new instance of A. Backstack is now A-B-A.
     - SingleTask: Only 1 instance of that activity at the same time. If no instance: create a new task with that activity as the root. Else if there is an instance in another task, system routes the intent to that instance through `onNewIntent()`.

* **Passing data between fragments** - [Learn from here](https://proandroiddev.com/android-fragments-fragment-result-805a6b2522ea)


#### Views

* **How can you measure measure/layout performance** - [Learn from here](https://android-developers.googleblog.com/2017/08/understanding-performance-benefits-of.html)
    - `FrameMetrics` API.
    
* **&lt;include&gt;,  &lt;merge&gt; tag**

* **How view renders?** - [Learn from here](https://medium.com/better-programming/understand-how-view-renders-in-android-763f0adfb95c)

* **Android internals for rendering a view?** - [Learn from here](https://medium.com/better-programming/android-internals-for-rendering-a-view-430cd394e225)

* **Overdraw?** - [Learn from here](https://developer.android.com/topic/performance/rendering/overdraw)
    - Refers to the system's drawing a pixel on the screen multiple times in a single frame of rendering. For example, if we have a bunch of stacked UI cards, each card hides a portion of the one below it.
    - Another source of overdraw: rendering transparent pixels (eg, any kind that involves **transparency**: shadows, fade-outs...).


* **Should we call `invalidate()` frequently for views?** - [Learn from here](https://developer.android.com/training/custom-views/optimizing-view?hl=en)
    - Use alternative methods like `postInvalidate()`, `postInvalidateOnAnimation()`, etc.

* **Adaptive icons** - [Learn from here](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=en)
    - Introduced from android 8.0, which can display a variety of shapes accross different devices.

* **Outline provider** - [Learn from here](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=en)
    - Used to clip views, which will change views's casting shadow.
    - When set to null, view won't have shadow.

* **`AnimatedImageDrawable` and `AnimatedVectorDrawable`** - [Learn from here](https://developer.android.com/about/versions/pie/android-9.0#animation)
    - They works simillarly in that the render thread drives the animations. And the render thread also uses a worker thread to decode.

* **ImageDecoder** - [Learn from here](https://developer.android.com/about/versions/pie/android-9.0#decoding-images)
    - Can handle gifs, WebP (which it will return an AnimatedImageDrawable).
    - Can decode image from byte buffer, file or URI.
    - Can perform post-processing, error handling, cropping, scaling.


#### Performance

* **Doze and App Standby** - [Learn from here](https://developer.android.com/training/monitoring-device-state/doze-standby?authuser=1)

* **FlatBuffers** - [Learn from here](https://engineering.fb.com/2015/07/31/android/improving-facebook-s-performance-on-android-with-flatbuffers)
    - Access to serialized data without parsing/unpacking: represents hierarchical data in a flat binary buffer in such a way that it can still be accessed directly without parsing/unpacking.
    - Memory efficiency and speed.
    - Flexible: offers optional fields: has backward compatibility.
    - Strongly typed.

#### Thread & Process

* **Process** - [Learn from here](https://developer.android.com/guide/components/processes-and-threads)
    - By default, all components of the same application run in the same process. However, if you find that you need to control which process a certain component belongs to, you can do so in the manifest file.
    - Interprocess communication(IPC): [Learn from here](https://developer.android.com/guide/components/processes-and-threads#IPC)


* **Thread** - [Learn from here](https://developer.android.com/guide/components/processes-and-threads)
    - Main thread: - [Learn from here](https://developer.android.com/guide/components/processes-and-threads)
        - In charge of dispatching events to the appropriate user interface widgets, including drawing events.
        - All components that run in the same process are instantiated in the UI thread, and system calls to each component are dispatched from that thread
    - Thread priority: - [Learn from here](https://developer.android.com/topic/performance/threads#main)
        - Threads in `foreground group` gets ~ 95% of total execution time for device.
        - A newly created one will with same priority and group memberships as spawning thread.
        - One cpu core can serve a process/thread at a time. Too many threads will go into `priority and scheduling` issue.
        - Kotlin's coroutine IO dispatcher allocates additional threads on top of the ones allocated to the default dispatchers to do IO-bound code (and hence fully utilize CPU resources).



#### Permissions

* **Install-time permission** - [Learn from here](https://developer.android.com/guide/topics/permissions/overview#install-time)

* **Run-time permission** - [Learn from here](https://developer.android.com/guide/topics/permissions/overview#runtime)

* **Special permission** - [Learn from here](https://developer.android.com/guide/topics/permissions/overview#special)
   

#### Android Versions

* **Android 11** - [Learn from here](https://developer.android.com/about/versions/11)
    - One-time permission.
    - Permissions auto-reset.
    - Update how media controls are displayed.
    - Chat bubbles.
    - Improve IME transitions.
    - Introduce Quick Access Device Controls feature: allows the user to quickly view and control external devices such as lights, thermostats, and cameras from the Android power menu.
    - Storage, location updates.
    - NN API 1.3.
    - NDK `ImageDecoder` API.

* **Android 10** - [Learn from here](https://developer.android.com/about/versions/10?authuser=2)
    - Foldables.
    - 5G.
    - Smart reply in notifications: uses on-device ML to suggest contextual actions like replies for messages or opening a map for an address in the notification. App can custom its own replies.
    - Dark theme: adds system-wide dark theme (ideal for low light/helps save battery). System can also create dark theme dynamically for apps (Force Dark feature).
    - Gesture navigation: eliminates nav bar, use edge swipes instead.
    - Settings panel: app can show key system settings(network, NFC, volume) directly in a floating panel.
    - Sharing shortcuts: let user jump directly to a specific activity in apps with content attached.
    - Privacy for users:
        - More control over location data: new permission option that allow app to access location only when foreground.
        - Preventing device tracking: apps can no longer access non-resettable ids like device serial number, etc. Device's MAC address is randomized when connected to WIFI.
        - Apps are given scoped access into external storage(don't need to request any storage-related permission): can see files in app-specific directory, medias that app created from media store.
    - Blocking unwanted interruptions: prevent app launches unexpectedly.
    

* **Pie (Android 9)** - [Learn from here](https://developer.android.com/about/versions/pie)
    - Display cutout support.
    - Notification enhancements: Users can reply/enter text directly from a notification, apps can display images in messaging notifications.
    - Multi-camera support and camera updates: access streams simultaneously from 2 or more physical cameras.
    - Introduces `ImageDecoder` for drawables and bitmaps:.
    - Introduces `AnimatedImageDrawable` for drawing and displaying GIF and WebP animated images.
    - Adds support for HDR VP9 profile.
    - Adds support for encoding images using High Efficiency Image File format(HEIF or HEIC), which improves compression and reduces storage space and network.
    - Data cost sensitivity for `JobScheduler`: can use network status to improve the handling of network-related jobs.
    - New rotation mode that lets user manually change device orientation by pressing a button in the system bar.
    - Added `Precomputed Text`: compute and cache required information ahead of time, and this will be performed off the main thread.
    - Limit access to sensors for background apps: cannot access mic/camera, or receive events from accelerometers, etc.
    - Other privacy changes: restrict access to phone numbers without permissions, access to wifi location and connection information.
    - Power management: [Learn from here](https://developer.android.com/about/versions/pie/power)
        - App Standby Buckets: system limits device resources(CPU, battery) available to each app based on which prioriy bucket the app is in (Active, Working set, Frequent, Rare, Never).
        - Battery saver improvements: background apps do not have network access, location service may be disabled when screen if off, etc.

* **Oreo (Android 8.0)** - [Learn from here](https://developer.android.com/about/versions/oreo/android-8.0?authuser=1)
    - Picture-in-picture.
    - Notifications:
        - Notification channels.
        - Notification dots.
        - Snoozing.
    - Autofill framework: helps fasten the process of filling in fields.
    - Downloadable fonts: apps can request fonts from a provider application instead of bundling fonts into APK. This will reduces APK size, allows multiple apps to use the same font, which will saves cellular data, phone memory and disk space.
    - Autosizing TextView.
    - Adaptive icons: can display a variety of shapes accross different devices.
    - Multi-display support: users can move an activity that supports multi-window to another display.
    - App categories: app can declare a category, which is used to group apps of similar purpose.
    - Neural Networks API (NNAPI).
    - Background execution limits:  
        - Background service limits: While an app is in background (does not have a visible activity or does not have a foreground service running/connected to it), system limits its use of background services(by killing those services when it goes into idle state).
        - Broadcast limits: apps can no longer register broadcast receiver in manifest for implicit broadcast(except some) because this may trigger many apps to consume resources. They can still register at runtime.
    - Background location limits: limits how frequently an app can retrieve location while running in background.
    - `SharedMemory` API: share data between apps or between multiple processes within a single app.

* **Nougat (Android 7.0)** - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.0?authuser=1)
    - Multi-window support.
    - Notification enhancements - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.0?authuser=1#notification_enhancements).
    - Improve Doze: applies some CPU and network restrictions on app even when device is not stationary. - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.0?authuser=1#doze_on_the_go)
    - Remove 3 implicit broadcasts: `CONNECTIVITY_ACTION, ACTION_NEW_PICTURE, ACTION_NEW_VIDEO`, as they can wake up background processes of multiple apps at once and hence not good for memory and battery.
    - SurfaceView: now has synchronous movement, which improves battery performance(composited in dedicated hardware).
    - Introduce Data Saver mode: enables user to control over the cellular data usage by apps.
    - Integrates Vulkan API into the platform.
    - Quick Settings Tile API: more room, can change what and where tiles are displayed.
    - Number blocking.
    - Support more languages.
    - Webview: ChromeAPK is used to render Android system webview.
    - OpenGL ES 3.2 API.
    - `FrameMetrics` API: allows to monitor UI rendering performance, by providing timing data that the rendering system reports.
    - Introduce App Shortcuts - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.1#shortcuts).
    - Image keyboard support: let user input images and other contents directly in a keyboard.
    - Storage manager intent: taking user to the system's free up space screen.

* **Marshmallow (Android 6.0)** - [Learn from here](https://developer.android.com/about/versions/marshmallow?authuser=1)
    - Introduce Run-time permission.
    - Doze and App Standby.
    - Apache HTTP Client Removal.
    - TextSelection: when user selects text, can show actions like copy, cut, etc in a floating toolbar.
    - App can no longer forced device to connect to a specific wifi network.
    - APK file is considered corrupt is a file is declared in manifest file but not present in the APK.
    - Camera: accessing shared resources in camera service prefer high-priority processes, and switch user will cause current camera client used by app to be evicted.

* **Lollipop (Android 5.0)** - [Learn from here](https://developer.android.com/about/versions/lollipop?authuser=1)
    - ART runtime: includes AOT compilation, improves garbage collection.
    - Improve audio and graphics pipelines.
    - View now have translation Z to have shadows.
    - Activity transitions.
    - `Vector drawables`.
    - Introduce heads-up notification: small floating window that allows the user to respond or dismiss without leaving the current app.
    - Multi-networking features: app can query for available networks, request a connection and respond to connectivity lost/gain.
    - Support for OpenGL ES 3.1.
    - Multi-channel audio stream mixing, new MediaSession API for controlling media playback.
    - From API >= 21: webview no longer allows mixed content and 3rd party cookies by default.

#### Network
* **Retrofit vs OkHttp** - [Learn from here](https://medium.com/mobile-app-development-publication/okhttp-or-retrofit-for-android-fc00f7aa3daf?source=email-43b67fe77107-1620847883634-digest.reader-f9c208bdbb09-fc00f7aa3daf----0-59------------------58c11afb_224d_41bf_b80d_279e917b7c2a-1-c616f544_7490_4b1b_9d4b_9f12fb602a64)
    - Retrofit:
        - Structured URL and parameter construction.
        - Received API response as our desired object model(by providing a GSON converter factory).
        - Put network call to background thread automatically and send result to main thread.
    - OkHttp:
        - Construct request manually
        ```java
            val request = Request.Builder().url("$BASE_URL$BASE_PATH/?" +
            "$PARAM_ACTION=$VALUE_QUERY&$PARAM_FORMAT=$VALUE_JSON&" +
            "$PARAM_LIST=$VALUE_SEARCH&$PARAM_SRSEARCH=$searchString")
            .build()
        ```
    
        - Deserialize the result ourselves: `result = Gson().fromJson(..., Result.class)`
        - API result is called on background thread.
        - More dynamic URL formation.


### Java And Kotlin

#### Java

* **StringBuffer vs StringBuilder** - [Learn from here](https://www.journaldev.com/538/string-vs-stringbuffer-vs-stringbuilder)

    | StringBuffer  | StringBuilder |
    | ------------- | ------------- |
    | Synchronized  | Not synchronized  |
    | Thread safe  | Not thread safe  |
    | Slower  | Faster  |

#### Kotlin

* **Coroutines** - [Learn from here](https://elizarov.medium.com/blocking-threads-suspending-coroutines-d33e11bf4761)
    - Suspending functions **do not** block the caller thread, but needed to use the `withContext(Dispatchers)`.

* **Coroutine Dispatchers** - [Learn from here](https://elizarov.medium.com/blocking-threads-suspending-coroutines-d33e11bf4761)
    - Default: optimized to do CPU-bound functions.
        - Backed by a thread pool with as many threads as there are CPU cores in system.
        - Does not over-allocate threads.
    - IO: optimized to execute IO-bound codes.
        - If a device has 4 core with 4 threads allocated to default dispatcher, and all of them are blocked in IO: our device is **under-utilized**.
        - Allocates addtional threads on top of the ones allocated to the **default dispatcher**, so can fully utilize machine's CPU resources and do blocking IO at the same time.

* **CPU-bound code vs IO-bound code** - [Learn from here](https://elizarov.medium.com/blocking-threads-suspending-coroutines-d33e11bf4761)
    - CPU-bound code: consume CPU resources.
    - IO-bound code: Does not actually consume CPU resources.

* **Inline function** - TBA
    - No runtime overhead.

* **Delegates** - [Learn from here](https://proandroiddev.com/kotlin-delegates-in-android-1ab0a715762d)
    - A class that provides the value for a property and handles its changes. This allows us to move, or delegate, the getter-setter logic from the property itself to a separate class, letting us reuse this logic.
    - Provided with the property it's working with via instance of KProperty class, and an object that has the property.

```Kotlin
class FragmentArgumentDelegate<T: Any> : ReadWriteProperty<Fragment, T> { }
```



### Tricky or unknown bugs

* **Add a new fragment, it has enter animation but does not have exit animation?** - [Reason](https://stackoverflow.com/questions/59434290/no-field-with-the-name-mlistener-is-found-in-animation-class)
    - Here's the logcat:

```Java
E/FragmentManager: No field with the name mListener is found in Animation class
    java.lang.NoSuchFieldException: No field mListener in class Landroid/view/animation/Animation; (declaration of 'android.view.animation.Animation' appears in /system/framework/framework.jar!classes3.dex)
        at java.lang.Class.getDeclaredField(Native Method)
        at androidx.fragment.app.FragmentManagerImpl.getAnimationListener(FragmentManager.java:1301)
        at androidx.fragment.app.FragmentManagerImpl.setHWLayerAnimListenerIfAlpha(FragmentManager.java:1283)
        at androidx.fragment.app.FragmentManagerImpl.moveFragmentToExpectedState(FragmentManager.java:1811)
        at androidx.fragment.app.FragmentManagerImpl.moveToState(FragmentManager.java:1852)
        at androidx.fragment.app.FragmentManagerImpl.executeOpsTogether(FragmentManager.java:2426)
        at androidx.fragment.app.FragmentManagerImpl.removeRedundantOperationsAndExecute(FragmentManager.java:2372)
        at androidx.fragment.app.FragmentManagerImpl.execPendingActions(FragmentManager.java:2273)
```




### Solutions

* **Achieve toolbar menu ripple effect** - [Learn from here](https://stackoverflow.com/questions/49884021/achieve-toolbar-menu-item-click-ripple-effect)
    - In short: `?attr/actionBarItemBackground`.

* **Make fading edge for a view** - [Learn from here](https://stackoverflow.com/questions/21888674/apply-fading-edges-to-imageview)
    - Look for the `getLeftFadingEdgeStrength()` and other relative methods.

* **Only allow to perform click on a portion of a custom view?**
    - Override `onTouchEvent()`. Remember to check if you actually need to handle (if your custom view does not set any click listener, and the parent view group has set a click listener to do something ...)

```java
@Override
    public boolean onTouchEvent(MotionEvent event) {
        // We draw everything in this view, so manually handle click if there is any click listener set to it (don't want it
        // to always consume touch event, if so, the touch event won't be passed to other views that is below this view)
        if (!hasOnClickListeners())
            return super.onTouchEvent(event);

        // Width is larger than visible content
        boolean insideTouchRegion = checkIfInsideTouchRegion(event);
        if (event.getActionMasked() == MotionEvent.ACTION_UP) {
            if (insideTouchRegion) {
                performClick();
            }
            return insideTouchRegion;
        }
        return insideTouchRegion;
    }
```


### AndroidX

* **Layout Res Id in constructor** - [Learn from here](https://medium.com/@miloszlewandowski/how-androidx-changes-the-way-we-work-with-activities-and-fragments-73b88d157678)
    - No longer needed to override `onCreate()/onCreateView()` in activity/fragment to set layout.

* **OnBackPressedDispatcher** - [Learn from here](https://medium.com/@miloszlewandowski/how-androidx-changes-the-way-we-work-with-activities-and-fragments-73b88d157678)
    - No longer needed to override `onbackPressed()` of activity to achieve logics you want, instead use this method in any place that has access to activity. This will gives more flexibility.

* **FragmentContainerView** - [Learn from here](https://medium.com/@miloszlewandowski/how-androidx-changes-the-way-we-work-with-activities-and-fragments-73b88d157678)
    - If using `FrameLayout` as a parent to your fragment, use this instead. It fixes some bugs include window insets dispatching.

* **How View model survives orientation change?** - [Learn from here](https://proandroiddev.com/the-curious-case-of-survival-of-viewmodel-afe074992fbc)
    - Using `NonConfigurationInstances` to get the saved `ViewModelStore`.
    - And yes, viewModel won't survive low memory or `finish()` scenarios, cause the viewModelStore will be cleared in those scenarios.





