# Validate input form

- \_formKey = GlobalKey\<FormState>()
- Form()
  - TextFormField()
    - validator: (value) {...}
  - \_formKey.currentSate.validate()

```dart
@override
Widget build(BuildContext context) {
  final _formkey = GlobalKey<FormState>();

  return Scaffold(
    child: Form(
      key: _formkey,
      child: Column(
        TextFormField(
          onChange: (value) {
            ...
          },
          validator: (value) {
            if (valueNotRight) {
              return 'something wrong';
            }

            return null; // when the value is correct.
          },
        ),
        TextFormField(
          onChange: (value) {
            ...
          },
          validator: (value) {
            ...
          },
        ),
        FlatButton(
          child: Text('Submit'),
          onPressed: () {
            if (_formKey.currentSate.validate()) {
              // do something when all values correct
            }
          },
        ),
      ),
    ),
  );
}

```
