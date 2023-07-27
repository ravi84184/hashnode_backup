---
title: "Adding Lottie Animation in Flutter: Elevate User Experience with Dynamic Animations"
datePublished: Thu Jul 27 2023 14:54:08 GMT+0000 (Coordinated Universal Time)
cuid: clkl9zd4y00000al9cne1diyh
slug: adding-lottie-animation-in-flutter-elevate-user-experience-with-dynamic-animations
canonical: https://medium.com/@ravipatel84184/adding-lottie-animation-in-flutter-elevate-user-experience-with-dynamic-animations-8774e5a3909a
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690469539009/59cd3add-a1ea-4d19-bea7-d93fa34c54df.gif

---

## **Introduction:**

Animations play a crucial role in creating engaging and delightful user experiences in mobile apps. Lottie, developed by Airbnb, is a powerful animation library that allows developers to integrate beautiful and interactive animations in their Flutter applications. In this blog, we will explore how to add Lottie animations in Flutter, enabling you to captivate your users and take your app’s visual appeal to the next level.

### **1\. Understanding Lottie Animation:**

Lottie is an animation library that renders After Effects animations in real time directly on mobile devices. It uses JSON files exported from After Effects to display vector-based animations with high fidelity. With Lottie, you can add dynamic animations to various UI elements, providing seamless and interactive experiences.

### **2\. Setting Up the Flutter Project:**

Before we begin, make sure you have a working Flutter project set up. If you haven’t already, install Flutter and create a new Flutter project using the following command:

```plaintext
flutter create lottie_animation_app
```

### **3\. Installing Required Packages:**

To use Lottie animations in your Flutter app, you’ll need to add the `lottie` package to your `pubspec.yaml` file:

```plaintext
dependencies:
  flutter:
    sdk: flutter
  lottie: ^2.5.0
```

Run `flutter pub get` to fetch the new dependency.

### **4\. Obtaining Lottie Animation Files:**

You can find many free and premium Lottie animation files on websites like LottieFiles ([lottiefiles.com](http://lottiefiles.com)). Download the JSON files that match your desired animations.

### **5\. Adding Lottie Animation to Your Flutter App:**

**Step 1:** Place the Lottie JSON File:

Copy the downloaded Lottie JSON file to the `assets` folder of your Flutter project.

**Step 2:** Display the Lottie Animation:

```plaintext
import 'package:flutter/material.dart';
import 'package:lottie/lottie.dart';

class LottieAnimationScreen extends StatefulWidget {
  const LottieAnimationScreen({super.key});

  @override
  State<LottieAnimationScreen> createState() => _LottieAnimationScreenState();
}

class _LottieAnimationScreenState extends State<LottieAnimationScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Lottie Animation in Flutter'),
      ),
      body: Center(
        child: Lottie.asset('assets/animation.json'),
      ),
    );
  }
}
```

Replace `'assets/animation.json'` with the actual path to your Lottie JSON file.

### **6\. Running the App:**

Run the app using the command `flutter run`, and you should see the Lottie animation displayed on the screen.

## Conclusion:

Congratulations! You’ve successfully added Lottie animation to your Flutter app, bringing life and interactivity to your user interface. Lottie allows you to create visually stunning animations that captivate your users and enhance their overall experience.

Experiment with various Lottie animations to match your app’s theme and purpose. From loading indicators to delightful illustrations, Lottie offers endless possibilities for elevating your app’s visual appeal.

Unleash the power of Lottie animation in Flutter and create unforgettable user experiences that leave a lasting impression!