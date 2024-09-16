---
title: "Implementing Dark Mode in Flutter: A Complete Guide"
seoTitle: "Flutter Dark Mode: Complete Implementation Guide"
seoDescription: "Learn how to implement dark mode in Flutter with this comprehensive guide. Step-by-step instructions for seamless UI transitions and user preferences."
datePublished: Mon Sep 16 2024 11:30:56 GMT+0000 (Coordinated Universal Time)
cuid: cm14xc9q4001a09mgbb334kyp
slug: implementing-dark-mode-in-flutter-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726486080071/43c21ccd-90b4-4fa2-b444-c2013d179a26.png
tags: flutter, dark-mode, darkmode, dark-web, fluttertheme, flutternik, devsnik, Dark, flutter-dark-theme

---

Dark mode has become an essential feature for modern apps, enhancing user experience by reducing eye strain, saving battery life, and giving a sleek, professional look. In Flutter, adding dark mode support is straightforward and provides flexibility in customizing themes. In this blog, we’ll explore how to implement dark mode in Flutter and ensure your app looks great in both light and dark themes.

### **Why Dark Mode?**

* **Reduced Eye Strain:** Dark backgrounds are easier on the eyes, especially in low-light environments.
    
* **Battery Efficiency:** On OLED screens, dark mode saves battery by reducing the power required to display light colors.
    
* **Improved Aesthetics:** Many users prefer dark themes for a cleaner, modern look.
    

### **Setting Up Themes in Flutter**

Flutter offers built-in support for light and dark themes, and you can easily toggle between them. Here’s how to get started:

#### **Step 1: Define Light and Dark Themes**

Start by defining both your light and dark themes in the `ThemeData` class. You can customize various aspects like primary colors, background colors, and text styles.

```dart
dartCopy codeThemeData lightTheme = ThemeData(
  brightness: Brightness.light,
  primaryColor: Colors.blue,
  backgroundColor: Colors.white,
  appBarTheme: AppBarTheme(
    backgroundColor: Colors.blue,
    titleTextStyle: TextStyle(color: Colors.white, fontSize: 18),
  ),
  textTheme: TextTheme(
    bodyText1: TextStyle(color: Colors.black),
  ),
);

ThemeData darkTheme = ThemeData(
  brightness: Brightness.dark,
  primaryColor: Colors.amber,
  backgroundColor: Colors.black,
  appBarTheme: AppBarTheme(
    backgroundColor: Colors.amber,
    titleTextStyle: TextStyle(color: Colors.black, fontSize: 18),
  ),
  textTheme: TextTheme(
    bodyText1: TextStyle(color: Colors.white),
  ),
);
```

#### **Step 2: Enable Theme Switching**

To allow users to toggle between light and dark modes, you can implement a switch in your app and update the theme accordingly. Use `MaterialApp` to apply the selected theme.

```dart
dartCopy codeclass MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool isDarkMode = false;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Dark Mode Example',
      theme: isDarkMode ? darkTheme : lightTheme,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Dark Mode in Flutter'),
        ),
        body: Center(
          child: Switch(
            value: isDarkMode,
            onChanged: (value) {
              setState(() {
                isDarkMode = value;
              });
            },
          ),
        ),
      ),
    );
  }
}
```

With this simple implementation, users can toggle dark mode on or off using a switch.

### **Using System Theme Settings**

Flutter can automatically adapt to the system’s theme settings (light or dark mode). By using `ThemeMode.system`, you can let the app reflect the user’s device settings.

```dart
dartCopy codeMaterialApp(
  theme: lightTheme,
  darkTheme: darkTheme,
  themeMode: ThemeMode.system, // Automatically switch based on system settings
);
```

### **Customizing Widgets for Dark Mode**

While Flutter’s `ThemeData` handles most styling, certain widgets may need manual customization for dark mode. For example, images or icons that don’t adjust well to dark backgrounds might need tweaking.

#### **Customizing Image Color in Dark Mode**

If your app uses images or icons, ensure they are visible on both light and dark backgrounds. You can dynamically adjust image color or brightness based on the theme.

```dart
dartCopy codeclass CustomImage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Image.asset(
      'assets/logo.png',
      color: Theme.of(context).brightness == Brightness.dark
          ? Colors.white
          : Colors.black,
    );
  }
}
```

### **Persisting User Preferences**

If you want the user’s theme preference (light or dark mode) to persist between app sessions, you can store it locally using `SharedPreferences`.

#### **Storing Theme Preference**

```dart
dartCopy codeclass ThemeNotifier with ChangeNotifier {
  bool _isDarkMode = false;
  bool get isDarkMode => _isDarkMode;

  ThemeNotifier() {
    loadTheme();
  }

  void toggleTheme() {
    _isDarkMode = !_isDarkMode;
    saveTheme();
    notifyListeners();
  }

  void saveTheme() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setBool('isDarkMode', _isDarkMode);
  }

  void loadTheme() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    _isDarkMode = prefs.getBool('isDarkMode') ?? false;
    notifyListeners();
  }
}
```

Then, you can use this theme notifier to persist the theme choice in your app.

### **Testing Dark Mode**

Testing dark mode is critical to ensuring your app provides a smooth experience in both themes. You can manually switch between themes during development by toggling the system’s theme settings or using the app’s theme switcher. Ensure that:

* Text is legible on both backgrounds.
    
* Images and icons are visible and correctly adjusted.
    
* Buttons and interactive elements are styled consistently.
    

### **Conclusion**

Implementing dark mode in your Flutter app is simple yet significantly enhances the user experience. By following best practices for theming and ensuring that your app adapts well to both light and dark environments, you can provide a modern, accessible, and visually appealing interface for your users.

Start adding dark mode support to your Flutter apps today, and give your users the flexibility they need!

Happy coding!