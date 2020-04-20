# "WebRTC Native Stack is considered as a single chain as close to the Hardware Abstraction Layer (HAL) as possible."


**Getting Started**
------

This repository involves a **[Step by Step Guide to Compile and Build WebRTC Library for Android](https://github.com/mail2chromium/Compile_WebRTC_Library_For_Android) based on WebRTC Native Stack.** As we all know, Android Programs run into *Dalvik Virtual Machine*. Native Development tool (NDK) allows users to execute some of the program using native code languages such as `C/C++`.

I have made this document pretty straight forward for those who are using WebRTC for the first time or for those who are still struggling to get most out of it. To get more details of WebRTC you have to look into this reference:

- [Android_Realtime_Communication_Using_WebRTC](https://github.com/mail2chromium/Android_Realtime_Communication_Using_WebRTC).

For *AudioProcessing* in Android, I will recommend you to must visit these references:

- [Android-Audio-Processing-Using-WebRTC](https://github.com/mail2chromium/Android-Audio-Processing-Using-WebRTC)
- [Android-Native-Development-For-WebRTC](https://github.com/mail2chromium/Android-Native-Development-For-WebRTC)

------

# Content of this Document:

------

- [Prebuilt Libraries](#prebuilt-Libraries)

- [Prerequisite Software](#prerequisite-Software)

- [Major Steps](#major-Steps)

- [Explanation of Steps](#Explanation-of-Steps)
  
  - [Getting the Code](#getting-the-Code)

  - [Dependencies and Branch Selection](#dependencies-and-Branch-Selection)

  - [Compilation and Building](#compilation-and-Building)
  
      - [Using AAR Build Tools](#using-AAR-Build-Tools)

      - [Using Manual Compilation](#using-Manual-Compilation)
      
- [Usage of Library](#usage-of-Library)

  - [Manually Include Packages](#manually-Include-Packages)(*.aar)

  - [Publish to Maven Repository](#publish-to-Maven-Repository)

- [Compilation Issues](#compilation-Issues)

- [Conclusion](#conclusion)

------

## Prebuilt Libraries:

------

The easiest way to get started is using the [official prebuilt libraries](https://bintray.com/google/webrtc/google-webrtc) available at JCenter. These libraries are compiled from the tip-of-tree and are meant for development purposes only.

On Android Studio 3+ add to your dependencies:

```
implementation 'org.webrtc:google-webrtc:1.0.+'
```

------

## Prerequisite Software:

------

#### Note: Android development is only supported on Linux.

So, I will must suggest to use any of *Linux-Environment* etc (`Ubuntu`) for Android Development. When you have setup your Linux-Environment, then make sure of these important things before hand:

- Hard-Disk Space around `30-50GB` (Minimum `20GB`)
- RAM `4-8GB` (Enough)
- Internet With Good `MBs`

Now open your terminal.

##### Strictly Recommended: Don't Open Multiple Terminal Tabs/Windows to install any of dependencies related to WebRTC Pre-requisites, Do Every of Your Task Related to WebRTC in One and Only One Terminal's Tab/Window.

Before to start with WebRTC Native Stack, first install these modules, using the following Commands:

     - sudo add-apt-repository ppa:openjdk-r/ppa
     - sudo apt-get install openjdk-8-jdk
     - sudo apt-get install pkg-config
     - sudo apt-get update


------

## Major Steps:

------

These are the only `11-Steps` which are basically the cream of WebRTC Native Development:

- To Get the Code
- To Compile and Build Library

I have explained about each step below in this document. To get basic understanding of these given steps see [Explanation of Steps](#explanation-of-Steps) and then start with these following steps one by one. 

##### Note: Every step takes its own time based on the *machine specs* and *internet speed*, so make sure every step is completed without interruption.

```
    1- git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
    
    2- export PATH="$PATH:${HOME}/depot_tools"
    
    3- mkdir webrtc_android
    
    3.1- cd webrtc_android
    
    4- fetch --nohooks webrtc_android
        
    5- gclient sync
    
    6- cd src/
    
    7- ./build/install-build-deps.sh
    
    8- git branch -r
    
    9- git checkout origin/master
    
    # To check you're in origin/master branch
    10- git branch
    
    11- tools_webrtc/android/build_aar.py

```

Now, if you look in the `webrtc_android/src/` directory, It turns out that you will end up with the compilation and building of `libwebrtc.aar`.

------

## Explanation of Steps:

------

The above mentioned `11-Steps` involve these three procedures to deal with:

##### - [Getting the Code](#getting-the-Code)

##### - [Dependencies and Branch Selection](#dependencies-and-Branch-Selection)

##### - [Compilation and Building](#compilation-and-Building)

------

### Getting the Code:

------

This procedure involves Steps from `Step-1` to `Step-5`, to get the native code of WebRTC from Google Git, there is always a need

- [To install the Chromium Depot Tools]()

Chromium and Chromium OS use a package of scripts called `depot_tools` to manage checkouts and code reviews.
The `depot_tools` package includes custom git binary, ninja build tools, gclient, gn, ninja, gcl, git-cl, repo, and others.

It is very easy to get these tools. Just take your first step by cloning the repository with this command:

```
    1- git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```

Now, its time to add path into *PATH Environment Variables*, so that the binaries/dependencies must be included in the repository. In this way, these binaries would be available in the current terminal:

```
    2- export PATH="$PATH:${HOME}/depot_tools"
```

If you close the current instance of Linux-terminal, then before starting any step (except step-1), you have to repeat this step to get working binaries in that instance. To get more detailed intuition, you can visit [Get Chromium Depot Tools](https://commondatastorage.googleapis.com/chrome-infra-docs/flat/depot_tools/docs/html/depot_tools_tutorial.html#_setting_up)

After this make a new directory and go into that directory using these commands:

```
    3-   mkdir webrtc_android
    3.1- cd webrtc_android
```

This is the directory, where all of your WebRTC Native Stack will be cloned and synced. Now, here comes the two *giant* steps of this getting code procedure which are:

- Fetch command is used to get the a regular WebRTC Native Source Code with the Android-specific parts added.
- Gclient Sync command is used to update your checkout for underlying source code i.e WebRTC Native Code.

Make sure your current directory is `webrtc_android/`:

```
    4- fetch --nohooks webrtc_android
    5- gclient sync

```

The `gclient sync` command will pull all dependencies of the Chromium src checkout. You will need to run this any time you update the main src checkout, including when you switch branches.

Try to avoid any kind of interruption as these processes may take enough time based on Machine Specs and Internet Speed because these processes require the android build chain tools for which;

#### Notice: It is to be Noted that the Android specific parts like the *Android SDK and NDK* are quite large **(~8 GB)**, so the total checkout size will be about **16 GB**.

After these steps, you will end up with Updated and Synced WebRTC Native Code.

------

### Dependencies and Branch Selection:

------

To install all required dependencies for linux, a script is provided for `Ubuntu`, which is unfortunately only available after your first `gclient sync`:

Make sure your current directory is `webrtc_android/src/`
```
    6- cd src/
    7- ./build/install-build-deps.sh

```

Most of the libraries installed with this script are not needed since WebRTC Developers now build using Debian sysroot images in build/linux, but there are still some tools needed for the build that are installed with [install-build-deps.sh](https://chromium.googlesource.com/chromium/src/+/master/docs/linux/build_instructions.md).
These all dependencies are very important to build the Native Source Code.

Here I will explain `Step-8,9`.Some of the developers recommend to look for particular git branches before Compiling the Native Source Code. To list down all the available WebRTC Checkout Branches use this command:

```
    8- git branch -r

```

You can see the available latest branches looks like this as follows:

![Latest_Branches](https://github.com/mail2chromium/Compile_WebRTC_Library_For_Android/blob/master/Branches.PNG)


Now you can checkout to the latest branch which is `branch-heads/m79`, using this command:

```
    9- git checkout branch-heads/m79

```

But I will must recommend you to checkout with the `origin/master`:

```
    9- git checkout origin/master

```

This will help you to resolve most of [compilation issues](#compilation-Issues). To get the details about your current branch you can simply use these commands:

```
    10- git branch
    or
    10- git status

```

------

### Compilation and Building:

------

There are two ways to compile the WebRTC Native Stack for Android to build the library i.e. `libwebrtc.aar`. You can use these following methods such as:

##### 1- [Using AAR Build Tools](#using-AAR-Build-Tools)

##### 2- [Using Manual Compilation](#using-Manual-Compilation)

------

### Using AAR Build Tools:

------

This is the most beautiful process. It would compile the source code for all supported CPU types such as

- arm64-v8a,
- armeabi-v7a,
- x86,
- x86_64

and at the end package all these *native libraries* and *.jar library* into `*.aar` file.

Make sure your current working directory is `webrtc_android/src/` of your workspace. Then run:

```
    11- tools_webrtc/android/build_aar.py

```

This process will take some time based on your machine specs and internet speed, so here we go:

![Builded_library](https://github.com/mail2chromium/Compile_WebRTC_Library_For_Android/blob/master/Build_Library.PNG)



Now, if you look in the `webrtc_android/src/` directory, It turns out that you will end up with the compilation and building of `libwebrtc.aar`.


------

### Using Manual Compilation:

------

This process will manually compile the source code for each particular CPU type. Manual Compiling involves these two steps:

##### 1- Generate projects using GN.

##### 2- Compile using Ninja

This step will compile library for both Debug and Release Mode of Development.

Make sure your current working directory is `webrtc_android/src/` of your workspace. Then run:

```
    11- gn gen out/Debug --args='target_os="android" target_cpu="arm"'
    11- gn gen out/Release --args='is_debug=false is_component_build=false rtc_include_tests=false target_os="android" target_cpu="arm"'

```
You can specify a directory of your own choice instead of out/Debug, to enable managing multiple configurations in parallel.

- To build for ARM64: use target_cpu="arm64"
- To build for 32-bit x86: use target_cpu="x86"
- To build for 64-bit x64: use target_cpu="x64"

For compilation you can simply use these following commands for (`out/Debug`, `out/Release`):

```
     11.1- ninja -C out/Debug
     11.1- ninja -C out/Release
```

The output of the above process will be in the `out/Debug` or `out/Release`. Manually compilation of the source code is quite difficult and challenging. As with, manual compilation you also need to package all these libraries into `.aar` manually which is more time consuming.

The Native `*.so` file will be in the lib.unstripped/, and the java `.jar` library will be in the `lib.java/` directory.

The Native `.so` library is un-stripped, you can strip it to *minimize file* size using strip tools for particular CPU type.
Such tools are located in this following Directory:

```
webrtc_android/src/third_party/android_ndk/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin/arm-linux-androideabi-strip (for x64 binary .so)

```



------

## Usage of Library:

------

You can use this (.aar) library into your project using:

##### - [Manually Include Packages](#manually-Include-Packages)(*.aar)

##### - [Publish to Maven Repository](#publish-to-Maven-Repository)


#### Manually Include Packages:

First kept your `libwebrtc.aar` file into the `libs` directory and then
open Project level `build.gradle` and include `flatDir` such as:

```

    allprojects {
        repositories {
            jcenter()
            flatDir {
                dirs 'libs'
            }
            google()
        }
    }


```

then, open Application Level `build.gradle` file and add `*.aar` file such as:

```
    dependencies {
        compile(name:'libwebrtc', ext:'aar')
    }

```

If everything goes well you will see library entry is made in build exploded-aar. Also note that if you are importing a .aar file from another project that has dependencies you'll need to include these in your build.gradle, too.

#### Publish to Maven Repository:

You can use maven to add `*.aar` libraries into the existing maven repository using this commands:

```
    sudo apt-get install maven
    mvn install:install-file -Dfile=./google-webrtc-M79.aar -DgroupId=com.aar.app -DartifactId=google-webrtc -Dversion=M79 -Dpackaging=aar -DlocalRepositoryPath=./libwebrtc-android -DcreateChecksum=true

```
Then you can add repository in the root gradle file followed by adding into your app module.


------

## Compilation Issues:

------

Some of you guys may try different branch-heads of WebRTC for there development. But I must suggest to use the `origin/master`. Because, it turns out that while using different branch heads, you may end up with multiple issues regarding `BUILD.gn` or inside this class `tools_webrtc/android/build_aar.py`, which may be an unhealthy experience.

Some kind of the issues are as follows:

##### 1- [Using AAR Build Tools](#using-AAR-Build-Tools)

![Error_of_AAR_Build Tools](https://github.com/mail2chromium/Compile_WebRTC_Library_For_Android/blob/master/issue_1.PNG)

##### 2- [Using Manual Compilation](#using-Manual-Compilation)

![Error_of_Manual_Compilation](https://github.com/mail2chromium/Compile_WebRTC_Library_For_Android/blob/master/issue_2.PNG)

And you may end up with same kind of many more issues. But if you have properly carried out the above steps, then hopefully, you won't be catch up with issue regarding Compilation and Building libraries. 

Now, If you have already completed your task to `step-7` with the whatever branch let's say in between (`branch-heads/60`--`branch-heads/m79`), then you can again select the `branch` of `origin/master` instead of any other `branch-heads`. To do that try these following steps:

Make sure you're in this directory `webrtc_android/src/`:

     - git checkout origin/master
     # To make sure you're using origin/master
     - git branch
     - gclient revert
     - gclient sync
     - tools_webrtc/android/build_aar.py

And hopefully, you will have your issues sorted, because currently, you are checking out a branch that is behind the `origin/master` and doesn't have all dependencies and modules over there which are necessary to build your `libwebrtc.aar`.


------
## Conclusion:
------

I have tried to get most out of it. Hopefully, If you will follow these steps properly. Again thanks to WebRTC-Developers for such as huge module for pre-processing as well as post-processing of Real-time Communication.
If you catchup with any kind of issues, feel free to jump into issues and open that one or you can simply use this discussion portal i.e [Discuss-webrtc](https://groups.google.com/d/forum/discuss-webrtc).
This group first verify your post, then display it after a short/long interval, so be relaxed. You're issue gonna be solved one day.
