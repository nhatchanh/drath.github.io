---
layout: post
title: "Up and running with PhoneGap"
modified:
categories: code
excerpt:
tags: [PhoneGap]
comments: true
image:
  feature:
date: 2015-10-09T08:08:50-04:00
---

This is not a blog on why hybrid applications are worth your time. There are other resources on the WWW that delve into this. This blog, however, is about how to get started making hybrid applications using PhoneGap. It's still not the easiest thing to do, and it still takes a couple of days to get everything setup just perfect for that next killer mobile app. This post aims to make that process a little less painful.

## Assumptions

While developing apps using PhoneGap works just as well on Windows or Linux operating systems, this blog assumes your development environment to be OS X. 

This is *not* about Adobe PhoneGap Build, which is cloud based solution for building PhoneGap projects. This is about building PhoneGap projects on you local development machine.

I assume you are comfortable with the Terminal command line. 

## Install Nodejs

A lot of the command line programs that are part of PhoneGap are based on nodejs, so installing nodejs is the first perquisite. [Download the installer](wwww.nodejs.org) and be done installing it. 

> Check: Once installation is completed, open a Terminal and run `node -v` and `npm -v`. Make sure the command runs, and the correct version is displayed.

## Install PhoneGap

In a Terminal, type the following commands to install PhoneGap, and then later on, to check that it installed correctly by printing out the version. Devendra

{% highlight bash %}
sudo npm install -g phonegap
{% endhighlight %}

> Check: Run `phonegap -v` from the Terminal and make sure the appropriate version is displayed.

## Install Homebrew

[Brew](http://brew.sh) is a package manager for installing packages in OS X. Paste the command below at a Terminal prompt:

{% highlight bash %}
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

> Check: Run `brew -v` from the Terminal and make sure it runs. Note down the version.

## Install Ant

The page on the [official ant page](http://ant.apache.org) describes ANT as a tool that is used to "build Java applications". We will need this tool too build Android apps. Run the following command to install it:

{% highlight bash %}
    brew install ant
{% endhighlight %}

> Check: Can you run `ant` from the Terminal? If yes, move to the next step.

## Install JDK and the Android SDK

The JDK and Android SDK is only needed if you're trying to make Android apps. If you only intend to use PhoneGap for iOS, skip this step altogether.

#### Install the JDK

- Download [Java SE Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) for your OS and double click the installer to install it.
- This will install **both** JRE and JDK. Run `java -version` to find out version of Java. At the time of writing this workshop, the version of java is 1.8.0.

Now, we need to install the Android SDK and tools. This is *error prone* and *time-consuming* so take your time to double check everything before moving to the next step.

#### Install Android SDK

{% highlight bash %}
    brew install android-sdk
{% endhighlight %}

The SDK will be installed inside **/usr/local/Cellar/android-sdk/[version]**. If simply typing `android` at the command line does not work, you may need to add this to the path. To do so, open ~/.bashrc and add the following line at the end of the file:

    export ANDROID_HOME=/usr/local/opt/android-sdk
    export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

Then run `source ~/.bash_profile` to update the environment variables.

#### Complete the SDK installation

We need more. Type the following command in a Terminal:

{% highlight bash %}
    android
{% endhighlight %}

This will launch the *Android SDK Manager* application. Note the path where the Android SDK is installed (it is displayed at the top of the window). 

1. Leave all the default checked items alone.
2. In addition, check the following packages:

    + **Android SDK Tools**. This will install ant scripts and the `ddms` tool.
    + **Android SDK Platform-tools**. This will install the `adb`  tool, useful for communicating with with emulator or a real Android phone connected via USB cable.
    + **Android SDK Build-tools** (latest version). This installs `aapt`, `dx`, and `zipalign`, tools needed for creating the final `apk`.
    + **Latest Android version**. At the time of writing, it is Android 5.1.1 (API 22). But make sure to **un-check** the following: 
        * "Documentation for Android SDK"
        * "Samples for SDK"
        * "Sources for Android SDK"
3. Click the install button. This will take some time! 

## Check progress

We're almost there. Make sure all the following commands run correctly. If not, go back and try to address them

{% highlight bash %}
java
javac
ant
android
adb
{% endhighlight %}

## Install XCode

If you will be building iOS apps, then of course XCode is needed. XCode can be installed from the App Store for free. Double click the installer to install Xcode on the system. 

## Install emulators

A real phone is the best option when it comes to testing PhoneGap apps. However, there are times when an emulator is just more convenient. The Android emulator that is bundled with the Android SDK is painfully slow. Watching paint dry is infinitely more pleasurable than watching the android emulator boot up. 

Luckily there is an alternative, and it is from [Genymotion](wwww.genymotion). The free version is perfectly usable for making all kinds of apps. Go ahead and install it. 

We don't need to install any emulators for iOS, because XCode has a really good simulator built right into the product.

## Create your first project

Create a new PhoneGap project. 

1. Open a new Terminal.
2. Create a directory called `Projects` inside your home directory using the `mkdir` command.
3. `cd` to the `Projects` directory.
4. Type `phonegap create helloworld com.example.helloworld HelloWorld` and hit enter. The project will be created.
5. A new directory is created. Type `cd helloworld` and hit enter to change to the directory.
6. Locate **config.xml** and open it. Change that value of the attribute `android-minSdkVersion` from 7 to 18. This step is **very important** without which the build will fail. 
7. Type `phonegap platform add android` to add the android platform to the project. If you are building for iOS the appropriate command is `phonegap platform add ios`.
8. `phonegap run android` to build and deploy the app to the simulator! Make sure the Genymotion emulator is running before running the command. For iOS, read on...

## Deploy the test android app to your phone

1. Why stop at the emulator? Connect your Android phone to the dev machine and type `adb devices` in the Terminal. You should see the phone listed as one of the devices. If you do not see it listed, disconnect and connect the phone again. If it still does show up, make sure your phone has [USB Debugging](http://www.kingoapp.com/root-tutorials/how-to-enable-usb-debugging-mode-on-android.htm) enabled.
2. Make sure the Genymotion emulator is *not* running.
3. In you phonegap app directory (`C:\Users\[username]\Projects\hello`) type `phonegap run android`. This time, the app will be deployed on to the phone!

## Deploy the iOS app

Deploying to a real iPhone is a lot more complicated process that involves certificates and iTunes accounts etc. Thankfully, the iOS simulator is pretty snappy so testing with a simulator is quite practical.

- Open XCode
- Open the .xcodeproj file 
- Build and run the project. The app will build and be deployed to the simulator built into XCode.

## Add to source control

Before you start making too many changes to the project it is important to add it to source control. It is usually to OK to just add the `www` directory to source control:

{% highlight bash %}
    git add www
{% endhighlight %}

## Miscellaneous

Running `phonegap run android` fails silently if there are errors during the build process. At such times, it is useful to run the following commands instead (say, if you were trying to build an Android app):

{% highlight bash %}
cd platforms/android/cordova
./clean
./build
./run
{% endhighlight %}

When running the above `./build` command you get the error that says "Ant is not found" you can install it by typing the following command:

{% highlight bash %}
    brew install ant
{% endhighlight  %}

## Digging into the project structure

| Name       | Type          | Purpose  |
| ------------- |:-------------:| -----
| config.xml      | file | Important file that is used to store configuration data used by the app. You will use this file frequently during development. 
| hooks     | directory | Custom scripts that will be called during various stages of the build process. Useful, but only in some specific circumstances. 
| platforms | directory | Completely generated by PhoneGap CLI during the build process. You almost **never** need to add any code in here manually.
| plugins | directory | Plugins are downloaded and installed from the command line and this where they reside. You almost **never** need to add any code to this directory, it is added automatically via the scripts.
| www | directory | This is where your application code resides. This is where the magic happens.

## List of commonly used commands

This is list of commands that are typically used during app development

| Description       | Command  |
| ------------- |:-------------:| -----
| Create a new project.      | `phonegap create com.example.helloWorld HelloWorld` 
| Add [android] platform.     | `phonegap platform add android` 
| Run project | `phonegap run android` 
| Build project (Alternate) | `./platforms/android/cordova/build`
| Add a plugin | `phonegap plugin add URL/fqdn`
|  Display all installed plugins. | `phonegap plugins ls`
|  Remove a plugin. | `phonegap plugins rm URL/fqdn`
|  List connected devices. | `adb devices`
|  Debug the program. | `adb logcat`

## Other helpful links

- [Installing PhoneGap](https://iphonedevlog.wordpress.com/2013/08/16/using-phonegap-3-0-cli-on-mac-osx-10-to-build-ios-and-android-projects/)
- [Android SDK Versions](https://developer.android.com/about/versions/android-4.3.html)

So what errors did you come across as you went down the rabbit hole of setting up PhoneGap? Leave a comment below!
