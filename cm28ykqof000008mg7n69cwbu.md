---
title: "Building Offline-First Flutter Apps with SQLite and Hive"
datePublished: Mon Oct 14 2024 11:56:18 GMT+0000 (Coordinated Universal Time)
cuid: cm28ykqof000008mg7n69cwbu
slug: building-offline-first-flutter-apps-with-sqlite-and-hive
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1728906882175/f608e4be-709d-4f24-b955-d8d9b7b7cc28.png
tags: sqlite, flutter-hive, flutternik, devsnik, ravi-patel-flutter, flutter-nik, flutter-storage, flutter-local-storage, flutter-sqlite, sqlite-storage, hive-storage, hive-local-storage

---

In today’s mobile world, users expect apps to work seamlessly, even when they don’t have a stable internet connection. An **offline-first architecture** allows apps to function effectively without relying on constant network availability, syncing data locally and pushing updates when the connection is restored. In this blog, we’ll explore how to implement an offline-first Flutter app using **SQLite** and **Hive** for local storage.

# **Why Offline-First?**

An offline-first approach offers several advantages:

* **Better User Experience**: Users can continue working without interruptions, even if they’re in areas with poor or no internet connectivity.
    
* **Data Persistence**: It ensures that user data remains available on the device, and updates are synced once the device reconnects to the internet.
    
* **Improved Performance**: Accessing and saving data locally is faster than fetching it from a remote server.
    

# **Step 1: Setting Up Local Databases (SQLite & Hive)**

In an offline-first architecture, you’ll need to store data locally on the user’s device. We’ll use SQLite for structured relational data and Hive for lightweight and fast key-value storage.

## **1\. SQLite for Structured Data**

SQLite is ideal for handling structured, relational data (like user profiles, tasks, or orders) in a Flutter app. Here’s how to set it up:

1. **Add SQLite to your Flutter project**: In your `pubspec.yaml`, add the following dependency:
    

```dart
dependencies:
  sqflite: latest_version
  path_provider: latest_version
```

2\. **Create Database Helper**: You’ll need a helper class to manage the SQLite database creation and CRUD operations.

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static final DatabaseHelper _instance = DatabaseHelper._internal();
  static Database? _database;

  factory DatabaseHelper() {
    return _instance;
  }

  DatabaseHelper._internal();

  Future<Database> get database async {
    if (_database != null) return _database!;
    _database = await _initDatabase();
    return _database!;
  }

  _initDatabase() async {
    String path = join(await getDatabasesPath(), 'app_database.db');
    return openDatabase(
      path,
      version: 1,
      onCreate: (db, version) {
        return db.execute(
            'CREATE TABLE tasks(id INTEGER PRIMARY KEY, title TEXT, completed INTEGER)');
      },
    );
  }

  Future<void> insertTask(Task task) async {
    final db = await database;
    await db.insert('tasks', task.toMap(),
        conflictAlgorithm: ConflictAlgorithm.replace);
  }

  Future<List<Task>> getTasks() async {
    final db = await database;
    final List<Map<String, dynamic>> maps = await db.query('tasks');
    return List.generate(maps.length, (i) {
      return Task(
        id: maps[i]['id'],
        title: maps[i]['title'],
        completed: maps[i]['completed'] == 1,
      );
    });
  }
}
```

## **2\. Hive for Key-Value Storage**

For lightweight, non-relational data such as user settings, preferences, or small datasets, Hive is an ideal choice.

1. **Add Hive to your project**: In your `pubspec.yaml`, add the Hive dependency:
    

```dart
dependencies:
  hive: latest_version
  hive_flutter: latest_version
```

2\. **Initialize Hive**: Before using Hive, initialize it in the `main.dart` file and define a data model for the type of data you’re going to store.

```dart
void main() async {
  await Hive.initFlutter();
  Hive.registerAdapter(UserPreferencesAdapter());
  runApp(MyApp());
}
```

3\. **Create Hive Box and Model**: Here’s how you create a Hive box to store user preferences:

```dart
import 'package:hive/hive.dart';

@HiveType(typeId: 0)
class UserPreferences extends HiveObject {
  @HiveField(0)
  bool darkMode;

  UserPreferences({required this.darkMode});
}
```

```dart
class PreferencesHelper {
  static Future<void> savePreference(UserPreferences preferences) async {
    var box = await Hive.openBox<UserPreferences>('preferencesBox');
    box.put('userPreferences', preferences);
  }

  static Future<UserPreferences?> loadPreferences() async {
    var box = await Hive.openBox<UserPreferences>('preferencesBox');
    return box.get('userPreferences');
  }
}
```

# **Step 2: Syncing Data with a Remote Server**

To ensure data is synced to the server once the device regains internet access, implement background sync operations. Flutter has a `connectivity_plus` package that can be used to monitor the device’s network state.

1. **Add connectivity\_plus**:
    

```dart
dependencies:
  connectivity_plus: latest_version
```

2\. **Detect Internet Connection**: Use `Connectivity` to detect when the device is online or offline and queue up tasks for syncing later.

```dart
import 'package:connectivity_plus/connectivity_plus.dart';

class NetworkHelper {
  static Future<bool> isConnected() async {
    var connectivityResult = await (Connectivity().checkConnectivity());
    return connectivityResult != ConnectivityResult.none;
  }
}
```

# **Step 3: Managing Sync Conflicts**

In an offline-first app, there may be conflicts when syncing data, especially if multiple changes occur while offline. You can handle these conflicts by:

1. **Timestamps**:  
    Add timestamps to each update, and apply the latest change when syncing.
    

```dart
final now = DateTime.now().millisecondsSinceEpoch;
await db.insert('tasks', {'title': 'New Task', 'updatedAt': now});
```

2\. **Conflict Resolution Logic**:  
Use logic to decide whether to overwrite or merge changes when the app comes back online.

# **Step 4: Implementing Background Sync**

Use a background service to continuously sync data in the background when the app isn’t actively in use.

1. **Using Flutter WorkManager**:  
    Add the `workmanager` package to schedule background tasks.
    

```dart
dependencies:
  workmanager: latest_version
```

2\. **Setting Up Sync Job**: Configure the WorkManager to periodically check for changes and sync with the server.

```dart
void callbackDispatcher() {
  Workmanager().executeTask((task, inputData) async {
    // Code to sync data with the server
    return Future.value(true);
  });
}

void main() {
  Workmanager().initialize(callbackDispatcher, isInDebugMode: true);
  Workmanager().registerPeriodicTask('1', 'syncTask', frequency: Duration(minutes: 15));
  runApp(MyApp());
}
```

# **Conclusion**

Building an offline-first Flutter app enhances user experience by ensuring smooth operation regardless of network status. By using SQLite and Hive for local storage, and syncing with a remote server when the connection is restored, you can offer users a reliable and efficient app that doesn’t lose functionality when offline.

#Flutter #OfflineFirst #SQLite #Hive #MobileDevelopment #DataSync #WorkManager #Connectivity #FlutterDatabase #FlutterStorage #AppDevelopment #Dart #FlutterNik