---
title: "Integrating Local Notifications in Flutter Using flutter_local_notifications Package"
seoTitle: "Integrating Local Notifications in Flutter"
seoDescription: "Learn how to integrate local notifications in Flutter using the flutter_local_notifications package. Step-by-step guide for enhanced user engagement!"
datePublished: Fri Oct 11 2024 11:56:30 GMT+0000 (Coordinated Universal Time)
cuid: cm24o9fkh00130cl2ewidhnth
slug: integrating-local-notifications-in-flutter-using-flutterlocalnotifications-package
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1728647069844/521de558-3751-4786-aedf-0f070ce10ae1.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1728647670535/41044324-d7d9-4771-b894-003fc89db07f.png
tags: flutter-push-notification, flutternik, flutterlocalnotifications, ravi-patel-flutter, ravi-patel, local-notification

---

Mobile apps often need to send notifications to users, whether it’s for reminding them of an event, notifying them about a new message, or delivering important information. Local notifications are an essential feature for apps that aim to engage users without requiring an active internet connection. Flutter, with its powerful plugin ecosystem, provides the `flutter_local_notifications` package to handle local notifications seamlessly.

In this blog, we’ll walk through the process of integrating local notifications into a Flutter app using the `flutter_local_notifications` package.

### 1\. What is the `flutter_local_notifications` Package?

The `flutter_local_notifications` package is a cross-platform plugin for displaying notifications in a Flutter app. It supports both iOS and Android and allows developers to send scheduled, repeating, and customizable notifications locally on the user’s device.

### 2\. Adding the `flutter_local_notifications` Package

To start using local notifications in Flutter, you first need to add the necessary package to your `pubspec.yaml` file:

```dart
dependencies:
  flutter_local_notifications: latest_version
```

Run `flutter pub get` to install the package.

### 3\. Platform-Specific Configuration

#### Android

To configure Android notifications, add the following permissions in your `AndroidManifest.xml` file located in `android/app/src/main/AndroidManifest.xml`:

```dart
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
```

This permission allows your app to handle notifications even after a device reboot. You’ll also need to configure the default notification icon in the `res/drawable` folder by creating a new image file and referencing it in `AndroidManifest.xml` like this:

```dart
<meta-data
  android:name="com.google.firebase.messaging.default_notification_icon"
  android:resource="@drawable/your_icon_name"/>
```

#### iOS

For iOS, you need to request permission to show notifications. To do this, modify the `Info.plist` file located at `ios/Runner/Info.plist`:

```dart
<key>UIBackgroundModes</key>
<array>
  <string>fetch</string>
  <string>remote-notification</string>
</array>
```

### 4\. Initializing Local Notifications

Before you can start showing notifications, initialize the plugin in your `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

void main() {
  runApp(MyApp());
}
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}
class _MyAppState extends State<MyApp> {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin;
  @override
  void initState() {
    super.initState();
    flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();
    var initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    var initializationSettingsIOS = IOSInitializationSettings();
    var initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);
    flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomeScreen(),
    );
  }
}
```

### 5\. Displaying a Simple Notification

Once initialized, you can create a simple notification:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
void showSimpleNotification() async {
  var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'your_channel_id', 'your_channel_name', 'your_channel_description',
      importance: Importance.max, priority: Priority.high, ticker: 'ticker');
  var iOSPlatformChannelSpecifics = IOSNotificationDetails();
  var platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics, iOS: iOSPlatformChannelSpecifics);
  await flutterLocalNotificationsPlugin.show(
    0,
    'Hello!',
    'This is a simple notification.',
    platformChannelSpecifics,
  );
}
```

This simple function sends a notification with the title “Hello!” and the message “This is a simple notification.”

### 6\. Scheduling Notifications

To send a notification at a specific time, you can use the following code to schedule it:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
import 'dart:async';
void scheduleNotification() async {
  var scheduledNotificationDateTime =
      DateTime.now().add(Duration(seconds: 5));
  var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'your_channel_id', 'your_channel_name', 'your_channel_description',
      importance: Importance.max, priority: Priority.high, ticker: 'ticker');
  var iOSPlatformChannelSpecifics = IOSNotificationDetails();
  var platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics, iOS: iOSPlatformChannelSpecifics);
  await flutterLocalNotificationsPlugin.schedule(
      0,
      'Scheduled Notification',
      'This notification was scheduled to show after 5 seconds.',
      scheduledNotificationDateTime,
      platformChannelSpecifics);
}
```

This notification will trigger 5 seconds after you call the function.

### 7\. Repeating Notifications

To create a repeating notification, you can use the `showDailyAtTime` or `showWeeklyAtDayAndTime` methods:

```dart
void showDailyNotification() async {
  var time = Time(10, 0, 0); // Set time to 10:00 AM
  var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'your_channel_id', 'your_channel_name', 'your_channel_description',
      importance: Importance.max, priority: Priority.high, ticker: 'ticker');
  var iOSPlatformChannelSpecifics = IOSNotificationDetails();
  var platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics, iOS: iOSPlatformChannelSpecifics);
await flutterLocalNotificationsPlugin.showDailyAtTime(
      0,
      'Daily Notification',
      'This notification will repeat every day at 10:00 AM.',
      time,
      platformChannelSpecifics);
}
```

This sends a daily notification at 10:00 AM.

### 8\. Customizing Notifications

You can customize notifications by adding a large icon, a sound, or vibration patterns to make them more engaging for users. For example, to add a custom sound:

```dart
var androidPlatformChannelSpecifics = AndroidNotificationDetails(
    'your_channel_id', 'your_channel_name', 'your_channel_description',
    sound: RawResourceAndroidNotificationSound('your_sound'),
    importance: Importance.max, priority: Priority.high);
```

Make sure to place your custom sound file in the `android/app/src/main/res/raw` folder.

### 9\. Handling Notification Taps

You can handle what happens when a user taps a notification by providing a callback function in the `initialize` method:

```dart
flutterLocalNotificationsPlugin.initialize(initializationSettings,
    onSelectNotification: (String payload) async {
  if (payload != null) {
    print('notification payload: $payload');
    // Navigate to a specific screen when tapped
  }
});
```

### 10\. Conclusion

The `flutter_local_notifications` package makes it easy to integrate and manage notifications in your Flutter app. With the ability to send simple, scheduled, and repeating notifications, this package provides all the essential tools for keeping users engaged with timely alerts.

Whether you’re building a to-do app that reminds users of tasks or a social app that notifies users of messages, integrating local notifications ensures a better user experience. Explore the various customization options and enhance your app’s functionality by leveraging the power of notifications!