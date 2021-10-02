# Save to local storage

Link [here](https://pub.dev/packages/shared_preferences)

---

Get the instance through out the app

```dart
final SharedPreferences prefs = await SharedPreferences.getInstance();
```

Set the preferences

```dart
prefs.setString('string', value);
prefs.setBool('bool', value);
prefs.setDouble('double', value);
prefs.setInt('int', value);
prefs.setStringList('string list', value);
```

Get the preferences

```dart
prefs.getString('string');
prefs.getBool('bool');
prefs.getDouble('double');
prefs.getInt('int');
prefs.getStringList('string list');
```
