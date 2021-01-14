# Android Cheatsheet

My cheatsheet which includes my experience working with Android development. This does not include the ones that are already mentioned at other sites.

You can also check for others's for more detail:\
    - https://github.com/MindorksOpenSource/android-interview-questions \
    - https://android.jlelse.eu/android-interview-questions-cheat-sheet-part-ii-bea0633f0da7
 
# Contents

* [Core Android](#core-android)
* [Java and Kotlin](#java-kotlin)
* [Tricky/unknown bugs](#bugs)
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


### Java And Kotlin
* **StringBuffer vs StringBuilder** - [Learn from here](https://www.journaldev.com/538/string-vs-stringbuffer-vs-stringbuilder)

    | StringBuffer  | StringBuilder |
    | ------------- | ------------- |
    | Synchronized  | Not synchronized  |
    | Thread safe  | Not thread safe  |
    | Slower  | Faster  |








### Tricky/unknown bugs





### Solutions

* **Achieve toolbar menu ripple effect** - [Learn from here](https://stackoverflow.com/questions/49884021/achieve-toolbar-menu-item-click-ripple-effect)
    - In short: ?attr/actionBarItemBackground.

* **Make fading edge for a view** - [Learn from here](https://stackoverflow.com/questions/21888674/apply-fading-edges-to-imageview)
    - Look for the getLeftFadingEdgeStrength() and other relative methods.




