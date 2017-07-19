---
layout: post
title: How to Debug Significant Location Change in iOS
date: 2017-04-23
---

# How to Debug Significant Location Change in iOS

Original Link : https://pawanpoudel.svbtle.com/how-to-debug-significant-location-change-code-in-ios

If an app has registered to listen for [significant location change notifications](http://goo.gl/1iE9PN), but is subsequently terminated, iOS will automatically relaunch the app into the background, if a new notification arrives. iOS generates significant location change notifications as soon as the device moves 500 meters or more from its previous notification location. These notifications don’t arrive more frequently than once every five minutes. Therefore, it could be challenging to test or debug code that handles these notifications without driving around with your device.

This article outlines steps you can follow in order to debug (or test)
[significant location change notifications](http://goo.gl/1iE9PN) using iOS
simulator and Xcode. We will use the [SignificantlyChanged](https://github.com/pawanpoudel/SignificantlyChanged) app as an example here, but you should be able to use the instructions listed here with any other app. SignificantlyChanged is a test app written specifically for this blog post. All it does is ask for user’s permission to use current location as soon as the app is launched. When the app goes to background, it registers for significant location change notifications. Finally, when the app is about to
enter foreground, it stops listening to those notifications.

**Step 1:** Open iPhone simulator (*Xcode > Open Developer Tool > iOS Simulator*).

**Step 2:** Reset simulator (*iOS Simulator > Reset Contents and Settings…*).

**Step 3:** Install *SignificantlyChanged* app on simulator. Allow the app to use your current location when asked.

**Step 4:** Click stop from Xcode (or use shortcut *⌘.*) to terminate *SignificantlyChanged*.

**Step 5:** Make sure location simulation is turned off (select *Debug > Location > None* from iOS Simulator).

**Step 6:** Launch app by tapping the app icon from iOS simulator

**Step 7:** Send app to the background (⌘⇧H). This will cause the app to register for significant location change notifications.

**Step 8:** Terminate the app

- Use **⌘⇧HH** key combination to launch the multitasking cards interface
- Click and hold the card for your app and then toss it up and away
- Use **⌘⇧H** key combination to go back to the home screen

**Step 9:** Edit *SignificantlyChanged* app’s scheme so that Xcode waits for the app to be launched manually.

[![edit_scheme.png](https://svbtleusercontent.com/qss6dirskbylmg_retina.png)](https://svbtleusercontent.com/qss6dirskbylmg.png)

[![wait_for_app_to_be_launched_manually.png](https://svbtleusercontent.com/12g1fwjnhip66q_retina.png)](https://svbtleusercontent.com/12g1fwjnhip66q.png)

**Step 10:** Set a breakpoint either inside the [application:didFinishLaunchingWithOptions:](http://goo.gl/HXCIIZ) method in app delegate or any other method that handles [UIApplicationDidFinishLaunchingNotification](http://goo.gl/KoK3sZ).

**Step 11:** Click run from Xcode (or use shortcut *⌘R*) to run *SignificantlyChanged* on simulator. You should see *Waiting for SignificantlyChanged to Launch* spinner.

[![waiting_for_app_to_launch.png](https://svbtleusercontent.com/4zuxzx6jljdya_retina.png)](https://svbtleusercontent.com/4zuxzx6jljdya.png)

**Step 12:** Put location simulation mode to freeway (select *Debug > Location > Freeway Drive* from iOS simulator)

- The freeway mode provides location simulation with enough speed for the simulator to generate significant location change notifications consistently.

**Step 13:** Wait for a notification to arrive. It should arrive within **5 minutes**. Once a notification arrives, your breakpoint (if you’ve set one) should be hit as shown in figure below.

[![app_did_finish_launching_break_point.png](https://svbtleusercontent.com/jg959lflxnu6uq_retina.png)](https://svbtleusercontent.com/jg959lflxnu6uq.png)