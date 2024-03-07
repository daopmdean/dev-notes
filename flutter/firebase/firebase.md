# Firebase

## Using firebase

Import firebase_core in pubspec.yaml before use

```yaml
firebase_core: ^0.5.0
```

Initialize firebase core

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(MyApp());
}
```

Import cloud_firestore to use firebase firestore

```yaml
cloud_firestore: ^0.14.0+2
```

```dart
void _onPressed() {
  firestoreInstance.collection("users").add(
  {
    "name" : "john",
    "age" : 50,
    "email" : "example@example.com",
    "address" : {
      "street" : "street 24",
      "city" : "new york"
    }
  }).then((value){
    print(value.id);
  });
}
```
