# Assets

```
your-app
├── android
├── assets
│   └── fonts
│   └── images
├── lib
├── ios
...

```

## Fonts

```yml
flutter:
  fonts:
    - family: Schyler
      fonts:
        - asset: assets/fonts/Schyler-Regular.ttf
        - asset: assets/fonts/Schyler-Italic.ttf
          style: italic
    - family: Trajan Pro
      fonts:
        - asset: assets/fonts/TrajanPro.ttf
        - asset: assets/fonts/TrajanPro_Bold.ttf
          weight: 700
```

## Images

```yml
flutter:
  assets:
    - assets/images/a_dot_burr.jpeg
    - assets/images/a_dot_ham.jpeg
```
