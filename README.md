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


### Core Android



#### Activity and Fragment

* **Some cases when activity's lifecycle transition to another** - [Learn from here](https://developer.android.com/guide/components/activities/state-changes)
     - Configuration change occurs, which can also triggered by language changing.
     - App enters multi-window mode and/or resized in this mode. Only the most recent activity that is interacted is in the onResume() state, the other is in onPause() state.
     - New activity/dialog appears in the foreground, taking focus and partialy/entirely cover the current activity. The current activity enters onPause()/onResume() respectively.

* **Activity launch modes** - [Learn from here](https://developer.android.com/guide/components/activities/tasks-and-back-stack)
     - SingleTop: If backstack contains A-B:
        - A new intent arrives for B, B is singleTop: B receives onNewIntent(). Backstack is now A-B.
        - A new intent arrives for A, A is singleTop: create new instance of A. Backstack is now A-B-A.
     - SingleTask: Only 1 instance of that activity at the same time. If no instance: create a new task with that activity as the root. Else if there is an instance in another task, system routes the intent to that instance through onNewIntent().


#### Views

* **How can you measure measure/layout performance** - [Learn from here](https://android-developers.googleblog.com/2017/08/understanding-performance-benefits-of.html)
    - FrameMetrics API.
    
* **&lt;include&gt;,  &lt;merge&gt; tag**

* **Should we call invalidate() frequently for views?** - [Learn from here](https://developer.android.com/training/custom-views/optimizing-view?hl=en)
    - Use alternative methods like postInvalidate(), postInvalidateOnAnimation(), etc.

* **Adaptive icons** - [Learn from here](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=en)
    - Introduced from android 8.0, which can display a variety of shapes accross different devices.

* **Outline provider** - [Learn from here](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=en)
    - Used to clip views, which will change views's casting shadow.
    - When set to null, view won't have shadow.


#### Performance

* **Doze and App Standby** - [Learn from here](https://developer.android.com/training/monitoring-device-state/doze-standby?authuser=1)


#### Permissions

* **Install-time permission** - [Learn from here](https://developer.android.com/guide/topics/permissions/overview#install-time)

* **Run-time permission** - [Learn from here](https://developer.android.com/guide/topics/permissions/overview#runtime)

* **Special permission** - [Learn from here](https://developer.android.com/guide/topics/permissions/overview#special)
   

#### Android Versions

* **Oreo (Android 8.0)** - [Learn from here](https://developer.android.com/about/versions/oreo/android-8.0?authuser=1)
    - Picture-in-picture.
    - Notifications:
        - Notification channels.
        - Notification dots.
        - Snoozing.
    - Autofill framework: helps faster the process of filling in fields.
    - Downloadable fonts: apps can request fonts from a provider application instead of bundling fonts into APK. This will reduces APK size, allows multiple apps to use the same font, which will saves cellular data, phone memory and disk space.
    - Autosizing TextView.
    - Adaptive icons: can display a variety of shapes accross different devices.
    - Multi-display support: users can move an activity that supports multi-window to another display.
    - App categories: app can declare a category, which is used to group apps of similar purpose.

* **Nougat (Android 7.0)** - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.0?authuser=1)
    - Multi-window support.
    - Notification enhancements - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.0?authuser=1#notification_enhancements).
    - Improve Doze: applies some CPU and network restrictions on app even when device is not stationary. - [Learn from here](https://developer.android.com/about/versions/nougat/android-7.0?authuser=1#doze_on_the_go)
    - Remove 3 implicit broadcasts: CONNECTIVITY_ACTION, ACTION_NEW_PICTURE, ACTION_NEW_VIDEO, as they can wake up background processes of multiple apps at once and hence not good for memory and battery.
    - SurfaceView: now has synchronous movement, which improves battery performance(composited in dedicated hardware).
    - Introduce Data Saver mode: enables user to control over the cellular data usage by apps.
    - Integrates Vulkan API into the platform.
    - Quick Settings Tile API: more room, can change what and where tiles are displayed.
    - Number blocking.
    - Support more languages.
    - Webview: ChromeAPK is used to render Android system webview.
    - OpenGL ES 3.2 API.
    - FrameMetrics API: allows to monitor UI rendering performance, by providing timing data that the rendering system reports.
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
    - Vector drawables
    - Introduce heads-up notification: small floating window that allows the user to respond or dismiss without leaving the current app.
    - Multi-networking features: app can query for available networks, request a connection and respond to connectivity lost/gain.
    - Support for OpenGL ES 3.1.
    - Multi-channel audio stream mixing, new MediaSession API for controlling media playback.
    - From API >= 21: webview no longer allows mixed content and 3rd party cookies by default.


### Java And Kotlin

* **StringBuffer vs StringBuilder** - [Learn from here](https://www.journaldev.com/538/string-vs-stringbuffer-vs-stringbuilder)

    | StringBuffer  | StringBuilder |
    | ------------- | ------------- |
    | Synchronized  | Not synchronized  |
    | Thread safe  | Not thread safe  |
    | Slower  | Faster  |








### Tricky or unknown bugs





### Solutions

* **Achieve toolbar menu ripple effect** - [Learn from here](https://stackoverflow.com/questions/49884021/achieve-toolbar-menu-item-click-ripple-effect)
    - In short: ?attr/actionBarItemBackground.

* **Make fading edge for a view** - [Learn from here](https://stackoverflow.com/questions/21888674/apply-fading-edges-to-imageview)
    - Look for the getLeftFadingEdgeStrength() and other relative methods.




