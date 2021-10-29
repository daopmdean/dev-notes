# ListView

```dart
// load all content in children include the one that is not visible
ListView(
  scrollDirection: Axis.vertical,
  children: [
    /*...*/
 ],
);
```

```dart
// only load what is visible
ListView.builder(
  padding: EdgeInsets.only(
    /*...*/
  ),
  itemCount: /*...*/,
  itemBuilder: (context, index) {
    return SomeThing(
      /*...*/
    );
  },
);
```
