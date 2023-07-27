---
title: "Why You Should Use Flutter for Your Projects"
seoTitle: "Why You Should Use Flutter for Your Projects"
seoDescription: "Why You Should Use Flutter for Your Projects"
datePublished: Fri Mar 31 2023 07:05:02 GMT+0000 (Coordinated Universal Time)
cuid: clfw79kbc000r0ajn732d2sj7
slug: why-you-should-use-flutter-for-your-projects
tags: flutter, flutter-cjxern4nz000zx6s1d95hxw7x, flutter-examples, flutter-widgets, flutternik

---

Flutter is a UI toolkit and SDK which you can use to build applications. Flutter is open source and you can use it to build highly performant mobile and desktop apps.

In this article, I'll explain in detail the various benefits of using Flutter so you can decide whether to use it for your next project.

## **Top Benefits of Flutter**

1. [Flutter is Cross-Platform](https://www.freecodecamp.org/news/why-you-should-use-flutter/#flutter-is-cross-platform)
    
2. [How Flutter is Cross-Platform](https://www.freecodecamp.org/news/why-you-should-use-flutter/#flutter-is-cross-platform)
    
3. [Flutter Has a Powerful UI Engine](https://www.freecodecamp.org/news/why-you-should-use-flutter/#flutter-has-a-powerful-ui-engine)
    
4. [How Flutter Renders UIs](https://www.freecodecamp.org/news/why-you-should-use-flutter/#how-flutter-renders-uis)
    
5. [Flutter Has Great State Management](https://www.freecodecamp.org/news/why-you-should-use-flutter/#flutter-has-great-state-management)
    
6. [Flutter Provides a Great Developer Experience](https://www.freecodecamp.org/news/why-you-should-use-flutter/#flutter-provides-a-great-developer-experience)
    
7. [Flutter Has a Wonderful Developer Community](https://www.freecodecamp.org/news/why-you-should-use-flutter/#flutter-has-a-wonderful-developer-community)
    
8. [Summary](https://www.freecodecamp.org/news/why-you-should-use-flutter/#please-use-flutter)
    

Now let's look at each of these features in more detail.

## **Flutter is Cross-Platform**

Software is cross-platform when it is available for different Operating Systems. You want your product to have such cross-platform ability so users on any device can use your product comfortably.

Having support for desktop, mobile, and web platforms is tough. For desktop, you will need to write code for macOS (with Swift), Linux (with C), and Windows (with C++). For mobile, you will need to write code for Android (with Kotlin/Java and XML) and iOS (with Swift).

To make your product accessible as a website, you have to use HTML, CSS, and JavaScript. Or, use any frontend JavaScript framework like Angular, React, or Vue.

Making applications for the various desktop and mobile operating systems requires separate SDKs and skillsets. In the past, you would've needed to hire developers who were proficient at each platform to implement your app on each of those platforms. This is expensive.

To add a feature, you would've needed to update the code across all these platforms which is tedious.

### **How Flutter is cross-platform**

Flutter code can run on desktop, mobile, and web platforms. So, you don't need to hire developers for each platform. You need to write the code only once in Flutter and you can rest assured that the app will work across the other platforms. So, Flutter is cheap.

Adding features to your app is fast because you only have to make code updates once in Flutter and that's all.

![demo](https://www.freecodecamp.org/news/content/images/2022/06/demo.gif align="left")

Same Flutter app working on desktop, mobile, and web.

The Flutter framework gives you APIs for painting and events (through widgets). It also provides APIs for platform-specific services (through method channels). So Flutter *exposes* *everything* to you to build the app in any way you want it. That's how cross-platform works.

![Screenshot--224--2](https://www.freecodecamp.org/news/content/images/2022/06/Screenshot--224--2.png align="left")

Adapted from [https://youtu.be/l-YO9CmaSUM](https://youtu.be/l-YO9CmaSUM)

Don't worry about performance. Naturally, Dart can compile to native code. So, the performance of Flutter apps is close (if not equal to) that of native apps.

[Dart's Ahead-Of-Time compiler](https://dart.dev/tools/dart-compile) is used to bundle the Flutter code. It is used when you launch the `flutter build` command. During the build step, only the app and the Flutter engine are shipped. This makes the built app small in size (very close to a native app).

## **Flutter Has a Powerful UI Engine**

UI rendering in Flutter is pixel-perfect. As a Flutter developer, you are in charge of every pixel painted on the device screen.

Flutter achieves this with the help of its engine. The Flutter engine is in charge of interpreting Flutter code to exactly what is drawn on the device's screen. Each Flutter app (built for any given platform) contains the engine which handles painting at runtime.

This also explains how Flutter is efficiently cross-platform, in terms of UI rendering. But this is more about the efficiency of the engine. The Flutter engine uses [Skia](https://skia.org/) for graphics. Skia is a 2D graphics library that handles graphics rasterization on various hardware and software.

The Flutter engine doesn't only contain Skia. It also has implementations of Flutter's core APIs (like texts and network I/O) at basic levels.

The Flutter engine is so powerful that it can efficiently re-render UIs at a speed of **60 frames per second** (60 fps). So when there are UI changes or animations, the engine makes them so fast as if it was a native application.

### **How Flutter Renders UIs**

Flutter uses composition aggressively. Composition here means widgets have widgets, which in turn have widgets, and so on. Everything in Flutter is a widget and Flutter UI code is essentially a big tree of widgets.

Behind the scenes, Flutter keeps **3 separate trees** for the UI. We normally code the outermost widget tree. In turn, the Flutter engine creates an *Element* and a *RenderObject* tree based on the widget tree.

In essence, each widget has its own corresponding Element and RenderObject. These last two entities are in charge of the actual representation of widgets on the device screen. Widgets themselves just hold the UI properties (like color, padding, shadows, and so on) that we set ourselves.

When UI is re-rendered, Flutter always destroys and rebuilds any changed widget (because widgets are immutable). However, it only replaces a linked Element or RenderObject *if need be.*

These extra UI trees explain how the widget tree is destroyed and rebuilt in each frame of the 60 fps rendering speed and yet the UI is re-rendered properly.

![widget_tree_1](https://www.freecodecamp.org/news/content/images/2022/07/widget_tree_1.png align="left")

The 3 UI trees, adapted from [https://youtu.be/996ZgFRENMs](https://youtu.be/996ZgFRENMs)

![widget_tree_2](https://www.freecodecamp.org/news/content/images/2022/07/widget_tree_2.png align="left")

The 3 UI trees with the Center widget as an example. Adapted from [https://youtu.be/996ZgFRENMs](https://youtu.be/996ZgFRENMs)

## **Flutter Has Great State Management**

State refers to data that your application needs to render its UI at any point in time. It could be user-generated or from your servers or backend.

In general, Flutter has two types of widgets: StatelessWidgets and StatefulWidgets. Anytime you will need to update the UI based on state, simply use a StatefulWidget ahead of time. Then to update the UI, call `setState()` anywhere inside the State class of a StatefulWidget and Flutter will rebuild the UI tree.

This `setState()` mechanism turns out to be the most efficient out there. It is also the React style of updating UI based on state. UI programming should be declarative and `setState()` simply advocates that.

You should call `setState()`  after asynchronous code has been executed (if any). This is because it is part of the main UI thread and blocking calls can hijack the UI rendering process.

If you have processes that are highly CPU intensive in a Flutter app, consider using [Dart Isolates](https://dart.dev/guides/language/concurrency#how-isolates-work) to carry out those processes, then call `setState()` with the data you get when processing is complete.

Sometimes, you may need access to state not scoped to a particular widget. At that point, you need a State Management architecture. There are a good number of them to choose from. These architectures provide state at an app-wide level without reconfiguring in each widget.

[Available options](https://docs.flutter.dev/development/data-and-backend/state-mgmt/options) include Provider, Riverpod, Redux, InheritedWidget, [Stacked](https://filledstacks.com/), and many more.

Another advantage of these architectures is that a good number of them permit good [separation of concerns](https://en.m.wikipedia.org/wiki/Separation_of_concerns) and [dependency injection (or inversion of control)](https://en.m.wikipedia.org/wiki/Dependency_injection).

In simpler terms, separation of concerns gives you the ability to write UI-specific code separate from logic-specific code. This way, if you want to debug, or change the packages or APIs you're using, you'll do them easily from one place (without fear of damaging the codebase). Besides, it promotes clean code too.

Dependency Injection involves the use of services or something similar to obtain what widgets need to work without the widgets configuring the services themselves. Some architectures like Stacked permit you to manage app-wide states without the BuildContext.

This pattern is useful because, in StatelessWidgets, the BuildContext is available only within the build method and you might need to use stuff outside it. So you could do other things like BottomSheet, Navigation, Toast, and so on without BuildContext.

## **Flutter Provides a Great Developer Experience**

There are many reasons the developer experience with Flutter is awesome. Here are a few of them:

### **Flutter has only one programming language – Dart.**

Programming on its own is a demanding activity. Frameworks, libraries, and tools shouldn't make coding tougher.

When coding for some platforms you usually write code in more than one programming language. For example, while coding for frontend web, you will alternate between HTML, CSS, and JavaScript files to manage a given portion of your webpage.

Flutter makes coding easy because you write in just one programming language: Dart. So most of the time, the logic and UI properties for a given portion of your Flutter app will be in the same Dart file.

Also, Flutter and Dart are written in plain English. Widget names and their properties reflect what they are. While coding Flutter, you are less likely to have any headaches understanding a given widget and or its use case(s).

### **Flutter has hot-reloading.**

Dart is a modern programming language that comes with [an Ahead-Of-Time (AOT) and a Just-In-Time (JIT) compiler.](https://dart.dev/tools/dart-compile)

The JIT compiler gives the feel that Dart is rather interpreted in runtime. In other words, it makes it possible for changes to Dart files to reflect immediately without needing to recompile the file, as is the case with some programming languages like C or Java.

Flutter leverages the JIT for development. Flutter ships a [Dart VM](https://mrale.ph/dartvm) to the platform in which the app's code is hosted. That way, when you launch the `flutter run` command, pressing `r` in that terminal ships in the changes in dart files, without recompiling the whole app. This instantaneous, yet *cross-platform* change-reflecting feature of Flutter is called **hot-reloading**.

Flutter also has **hot-restarting**. Hot restarting is achieved by pressing `R` (uppercase instead of lowercase this time). *Hot restarting* restarts the app entirely.

You need to do a hot-restart instead if you change some important parts of the Flutter code. For example, changing `class` declarations or their superclasses will need a hot restart.

### **Flutter is universal.**

Flutter is available for each Operating System. So you won't need to migrate or use a particular Operating System to create apps with Flutter as is the case with iOS apps (where you need an Apple computer).  

Flutter smoothly integrates with popular IDEs. Android Studio, IntelliJ, and VS Code (Visual Studio Code) have plugins or extensions for Flutter. So you can manipulate Flutter commands directly in the IDE without using the terminal.

![demo2](https://www.freecodecamp.org/news/content/images/2022/06/demo2.gif align="left")

Editing Flutter as an Android app in Android Studio 

![demo3](https://www.freecodecamp.org/news/content/images/2022/06/demo3.gif align="left")

Editing Flutter as a Windows app in VS Code 

Android Studio is relatively demanding in terms of computing resources. If your laptop [is not up to 8GB RAM](https://developer.android.com/studio#system-requirements-a-namerequirementsa), don't feel left out.

Setting up Flutter auto-detects your Operating System and browsers. Flutter is available for the web (to run Flutter apps in browsers). So you can test Flutter code in your browser or as a desktop app if RAM or CPU capacity could be a problem.

There is also [dartpad.dev](http://dartpad.dev), [flutlab.io](http://flutlab.io), and [flutterflow.io](http://flutterflow.io) that let you create Flutter apps online, in the browser. You will find these useful as they do not require as many computing resources as running Flutter for Android or iOS.

### **Flutter DevTools**

Dart naturally comes with a set of utilities for optimizing and debugging Dart code. This suite of tools is accessible from the browser or IDE you are using. While coding Flutter, using DevTools will shorten your coding time and give you deep insights into your app.

[Flutter DevTools](https://docs.flutter.dev/development/tools/devtools/overview) include indispensable tooling like an inspector, a debugger, a performance monitor, a network monitor, logger, and more.

![Screenshot--234-](https://www.freecodecamp.org/news/content/images/2022/07/Screenshot--234-.png align="left")

Flutter DevTools

## **Flutter Has a Wonderful Developer Community**

> The Flutter framework is relatively small... – [from the Flutter Docs](https://docs.flutter.dev/resources/architectural-overview)

![flutter_is_smalll](https://www.freecodecamp.org/news/content/images/2022/06/flutter_is_smalll.png align="left")

The Flutter team themselves acknowledge the community. In itself, the Flutter framework is relatively small compared to the entire Flutter ecosystem. Flutter is Open Source.

Around Flutter there are so many developers that have extended the framework. These developers have published more than 24,000 packages on [pub.dev](http://pub.dev). Each package has at least one widget you can import to your Flutter app.

If you have issues with Flutter or come across errors while using Flutter, you will find a solution once you search about it online. Chances are there are [GitHub issues](https://github.com/flutter/flutter/issues) or [Stackoverflow questions](https://stackoverflow.com/questions/tagged/flutter) on what you are looking for. Stackoverflow has a lot of Flutter developers willing to help you, so don't hesitate to ask questions with the Flutter tag.

[Flutter Groups](https://flutter.dev/community) and [GDG](https://developers.google.com/community/gdg)s are tech communities, found in various countries. Annually, these communities organize a Flutter-only event commonly known [FlutterFest](https://www.flutterfestival.com/). Some FlutterFest events are in person while some are virtual. These events bring the community members together for Flutter, Flutter, and more Flutter.

That said, you should use Flutter because you are not alone. You are confident that there are people around you that equally use it too and can help you when you are in need.

Also, maintenance and future support for Flutter look promising. [Fuchsia](https://fuchsia.dev/) is an upcoming open-source operating system. Asides from the current cross-platform support, Flutter for Fuchsia is available.

## **Summary**

In summary, use Flutter because of the many benefits you will gain.

You will have a cross-platform application whose UI is pixel perfect and state properly managed. You will also enjoy your development experience and will leverage the Flutter community.  

Cheers to the many Flutter apps you will build.

## **Helpful Resources**

* [How is Flutter different for app development](https://youtu.be/l-YO9CmaSUM)
    
* [How Flutter renders Widgets](https://youtu.be/996ZgFRENMs)
    
* [Flutter Architectural Overview](https://docs.flutter.dev/resources/architectural-overview)
    
* [List of state management approaches](https://docs.flutter.dev/development/data-and-backend/state-mgmt/options)
    
* [How to Implement any UI in Flutter](https://www.freecodecamp.org/news/how-to-implement-any-ui-in-flutter)