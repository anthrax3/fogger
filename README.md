 
![fog](https://stash.office/projects/MAS/repos/android-blur/browse/example/res/drawable/icon.png?at=2e95cffd43e15feb9651bc9587507e56394b850a&raw "fog")  
Fogger
====================

Lib to create blurred background under:
* dialogs
* drawer
* context menu

Features
--------------------
You can blur view behind drawer, dialog window and context menu.

![example](https://stash.office/projects/MAS/repos/android-blur/browse/readme/fog-example.gif?at=859b9358da5b852327a392940486d9842d361f75&raw "Example")


How to get it
--------

Grab via Maven:
```xml
<dependency>
  <groupId>pl.allegro.android</groupId>
  <artifactId>fogger</artifactId>
  <version>1.0.0</version>
</dependency>
```
or Gradle:
```groovy
compile 'pl.allegro.android:fogger:1.0.0'
```

Motivation
--------
All over the internet there are pieces of code that show how to make blur effect on Android. But there is not any
library that helps you to blur background under mostly used UI items. I want to make it as easy to use as possible so
you do not have to change architecture of you app.

Examples
===================
Drawer 
-------------------
To make drawer with fluent, blurred you have to provide only two changes to standard Android drawer. 
At the first the root view must be ```pl.allegro.fogger.ui.drawer.DrawerLayoutWithBlurredBackground``` instead
of ```DrawerLayout```

The second modification is to add tag value 

```xml
 android:tag="fragmentPlaceholder"
``` 
 to main content layout. You could also use string resource id provided with aar
 ```xml
  android:tag="@string/view_with_drawer_tag"
  ```
   
The full example:
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   
   <pl.allegro.fogger.ui.drawer.DrawerLayoutWithBlurredBackground
           xmlns:android="http://schemas.android.com/apk/res/android"
           android:id="@+id/drawer_layout"
           android:layout_width="match_parent"
           android:layout_height="match_parent">
           
       <FrameLayout
           android:id="@+id/fragmentPlaceholder"
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:tag="@string/view_with_drawer_tag"/>
   
       <FrameLayout
               android:id="@+id/drawer_container"
               android:tag="@string/drawer_content_view_tag"
               android:layout_width="240dp"
               android:layout_height="match_parent"
               android:layout_gravity="start">
               <include layout="@layout/settings"/>
       </FrameLayout>
       
   </pl.allegro.fogger.ui.drawer.DrawerLayoutWithBlurredBackground>
   ```
Working example of drawer with dynamically blurred background you could find in the [example app](https://stash.office/projects/MAS/repos/android-blur/browse/example)

Dialog
-------------------

Showing dialog with blurred background is as simply as showing traditional Dialog window.
All you have to do is use special dialog launcher.

```java
public class MyActivity extends Activity {

 ...
 
     public void showDialog() {
         DialogWithBlurredBackgroundLauncher dialogWithBlurredBackgroundLauncher
                     = new SimpleDialogWithBlurredBackgroundLauncher(this);
             Dialog dialog = new Dialog(this);
             dialog.setTitle(R.string.example_dialog_title);
             dialogWithBlurredBackgroundLauncher.showDialog(dialog);
     }
 }
```
As you can see, it is just one more line of code compare to dialog window with standard background.

Working example of dialog window with blurred background you could find in the [example app](https://stash.office/projects/MAS/repos/android-blur/browse/example)

Context Menu
-------------------
To create context window with blurred background you must prepare ```Activity``` that extends 
```java
public abstract class ActivityWithContextMenu extends Activity {
``` 

then you must implements one required abstract method
```java
    protected abstract int getContextMenuResId(View view);
```

The method must provide resource id form context menu to show eg.
```java
    @Override
    protected int getContextMenuResId(View view) {
        return R.menu.context_menu;
    }
```
The rest of context menu flow is unchanged, so you have to register context menu on some View and listen click event with Androids method
```java
public boolean onContextItemSelected(MenuItem item) {
```


Road Map
===================
At the moment I have no plan for further features, if you have any idea please let me know.

License
=======

    Copyright 2014 original author or authors

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
