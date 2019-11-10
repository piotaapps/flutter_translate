[<img src="https://github.com/bratan/flutter_translate/raw/master/resources/images/flutter_translate.png" />](https://github.com/bratan/flutter_translate/)

[![Build Status](https://travis-ci.org/bratan/flutter_translate.svg)](https://travis-ci.org/bratan/flutter_translate)
[![pub package](https://img.shields.io/pub/v/flutter_translate.svg?color=important)](https://pub.dev/packages/flutter_translate)
<a href="https://github.com/Solido/awesome-flutter">
   <img alt="Awesome Flutter" src="https://img.shields.io/badge/Awesome-Flutter-blue.svg?longCache=true" />
</a>
[![License: MIT](https://img.shields.io/badge/License-MIT-ff69b4.svg)](https://github.com/bratan/flutter_translate/blob/master/LICENSE)
[![Flutter.io](https://img.shields.io/badge/Flutter-Website-deepskyblue.svg)](https://flutter.io/)

---

The internationalization (i18n) library for Flutter.

It lets you define translations for your content in different languages and switch between them easily.

## Example
<img src="https://raw.githubusercontent.com/bratan/flutter_translate/master/resources/gifs/flutter_translate_screen.gif" width="300"/>

## Table of Contents
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Usage](#usage)

## Installation

Add this to your package's pubspec.yaml file:

```sh
dependencies:
  flutter_translate: ^1.5.1
```

Install packages from the command line (or from your editor):

```sh
flutter pub get
```

## Configuration

Import flutter_translate:

```dart
import 'package:flutter_translate/flutter_translate.dart';
```

Place the *json* localization files in a folder of your choice within the project.

By default ```flutter_translate``` will search for localization files in the `assets/i18n` directory in your project's root.

Declare your assets localization directory in ```pubspec.yaml```

```sh
flutter:
  assets:
    - assets/i18n
```

In the main function create the localization delegate and start the app, wrapping it with LocalizedApp

```dart
void main() async
{
  var delegate = await LocalizationDelegate.create(
        fallbackLocale: 'en_US',
        supportedLocales: ['en_US', 'es', 'fa']);

  runApp(LocalizedApp(delegate, MyApp()));
}
```

If the assets directory for the localization files is different than the default one (```assets/i18n```), you need to specify it:

```dart
 var delegate = await LocalizationDelegate.create(
      ...
        basePath: 'assets/i18n/'
      ...
```

Example MyApp:

```dart
class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {

    var localizationDelegate = LocalizedApp.of(context).delegate;

    return LocalizationProvider(
      state: LocalizationProvider.of(context).state,
      child: MaterialApp(
        title: 'Flutter Translate Demo',
        localizationsDelegates: [
          GlobalMaterialLocalizations.delegate,
          GlobalWidgetsLocalizations.delegate,
          localizationDelegate
        ],
        supportedLocales: localizationDelegate.supportedLocales,
        locale: localizationDelegate.currentLocale,
        theme: ThemeData(primarySwatch: Colors.blue),
        home: MyHomePage(),
        ),
      );
  }
}
```

## Usage

Translate a string:

```dart
translate('your.localization.key');
```

Translate with arguments;

```dart
translate('your.localization.key', args: {'argName1': argValue1, 'argName2': argValue2});
```

Translate with pluralization:

```dart
translatePlural('plural.demo', yourNumericValue);
```

JSON:

```json
"plural": {
    "demo": {
        "0": "Please start pushing the 'plus' button.",
        "1": "You have pushed the button one time.",
        "else": "You have pushed the button {{value}} times."
    }
}
```

Change the language:

```dart
@override
Widget build(BuildContext context) {
...
  ...
    changeLocale(context, 'en_US');
  ...
...
}
```

### You can view the full example here:

[https://github.com/bratan/flutter_translate/blob/master/example/lib/main.dart](https://github.com/bratan/flutter_translate/blob/master/example/lib/main.dart)
