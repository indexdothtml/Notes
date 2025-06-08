# Flutter and Dart Notes

## What is Flutter

Flutter is an open-source UI software development kit/UI Framework created by Google. It can be used to develop cross platform applications from a single codebase for the web, Fuchsia, Android, iOS, Linux, macOS, and Windows.

It bundles with UI Framework which contains code packages and utility functions for writing cross-platform app code and Collection of Tools - CLI and software that helps with developing, testing and building cross-platform apps.

To know internal working of Flutter - https://flutteris.com/blog/en/flutter-internals

## Dart langauge

Dart is a programing language used by Flutter to develop application. It is created by Google.
Google wants a language which can be optimized with Flutter framwork so they created Dart instead of using existing one.

The most popular usecase of Dart language is in Flutter framework but it can also be used in web development, back-end development, CLI development etc.

## main.dart file in lib

This file is starting point/entry point of Flutter project, it will generate full app, whenever you will execute the main.dart file.

## How to execute Flutter project

There are multiple ways:

1. Go to the `main.dart` file in `lib/` folder, and there you can see `Run| Debug | Profile` option above the `void main()` function, it is due to our Flutter extension, just click on `Run` and it will run your project.

2. Open the Terminal in VS Code, Go inside your project directory and type `flutter run` command.

3. Click on `Run` option from VS Code title bar and click on `Run Without Debugging` or press `ctrl + F5` in keyboard.

NOTE: Before you run your Flutter project, your emulator (if in android) or simulator (if in MacOs) should already set up. (How to - Go the command pallet of VS Code and type `Flutter: Launch Emulator` create new emulator if not exist or select any one)

## MaterialApp Widget

MaterialApp is widget in Flutter, which uses Material Theme created by Google, to design your app.

## How .dart file and Flutter executes app on platfrom like IOS and Android.

It will start with `main.dart` file, your main.dart file is compiled from top to bottom using dart compiler.
Then it is translated into the native machine code for Android (android native supporting code) and IOS (IOS native supporting code) by Flutter.
Then that translated code gets bundled together and shipped to respective platfrom, then platform understand that code and execute it.

## function defination and execution in dart

```dart
// Function defination
/*
    Syntax ->

    DataType FunctionName() {
        return ReturnValue; // If void DataType is not set.
    }
*/

void main() {
    //...
}

// Function execution
/*
    Syntax ->

    FunctionName();
*/

main();
```

## import in dart

1. Importing local code files.

```dart
// Syntax -> import 'path_to_the_file';

import 'utils/helper.dart';
```

2. Importing built-in dart libraries.

```dart
// Syntax -> import 'dart:Name_of_the_library';

import 'dart:math';
```

3. Importing external packages.

```dart
// you need to install external package first before using, install it by defining package name inside pubspec.yaml file
// Syntax -> import 'package:package_name';

import 'package:http/http.dart';
```

4. Importing limited, as required code instead of everything (use of "show").

```dart
// Syntax -> import 'path_to_the_library' show function1, function2;

import 'dart:math' show pi, sqrt; // only import pi and sqrt from math library
```

5. Importing everything instead of (use of "hide").

```dart
// Syntax -> import 'path_to_the_library' hide function1, function2;

import 'dart:math' hide pi, sqrt; // import everyting except pi and sqrt.
```

6. importing with alias (useful with avoiding name conflicts)

```dart
// Syntax -> import 'path_to_the_library' as lib1;

import 'dart:math' as mathlib; // now math library reffered as mathlib, use like mathlib.pi
```

7. importing with deferred (importing lazily)

```dart
// Syntax -> import 'path_to_the_library' deferred as lib1;

import 'dart:math' deferred as mathlib;
```

## main function in dart

`main()` is a special type of function, which you will write at very first time in main.dart file.
It is invoked/called by Flutter itself so developer no need to call it manually.
It is starting point of execution of your dart code, which can call `runApp()` another function inside it.

## runApp function in dart

`runApp()` function tells Flutter which widget to draw onto the screen.

runApp attaches widget tree to given screen, Flutter UI is created with combination and nesting of different widgets, it will be built-in widgets and custome widgets.

runApp function takes one argument, which is Widget, most of the time main widget which can sturcture your app like `MaterialApp` widget (MaterialApp widget takes arguments which can define your look of the app).
For ex - runApp(MaterialApp());

## Widget in Flutter

A widget is the fundamental building block of the user interface in Flutter app. Everything you see on the screen in a Flutter app is a widget, including structural elements (like buttons or text), stylistic elements (like fonts or colors), and layout elements (like padding or rows).

## MaterialApp widget

MaterialApp widget that wraps a number of widgets that are commonly required for Material Design applications.
MaterailApp widget setup the app.
`home` named argument is required, which contains tree of widgets.

For ex -

```dart
MaterialApp(
    home: Scaffold(body: Center(child: Text("Hello World!!!"))),
),
```

## Positional argument and Named argument in Dart

Arugments passing to the function can be positional like mostly used in other programming language function call or like Named argument which is most common in Flutter.

Postional argument -

```dart
void func(a, b) {
    // here a and b are positional parameters, the arguments should be passed in order to correctly work.
}

func(valueA, valueB); // arguments are passed in order to the function first value for a and then b.
```

Named argument -

```dart
void func({a, b}) {
    // here a and b are named argument written like above inside {} symbol.
}

func(b: valueB, a: valueA) // while calling it is not matter with order you are passing argument. In Flutter all the widgets uses named argument approch.
```

Postional arguments are not optional by default, you have to pass all arguments, but you can make it optional using [] symbol around parameter, also you can pass default value to optional parameter like. [b = 2] here 2 is default value

```dart
func(a, [b]) {
    // b is optional now
}

func2(a, [b = 2]) {
    // b has default value 2
}
```

Named arguments are optional by default, but you can make it required using required keyword.

```dart
func({required a, required b}) {
    // here a and b are not optional.
}
```

## 'const' keyword

In general programming, as we know 'const' keyword is used to avoid re-declaration of variable or function in memory, instead using it without re-declaring or changing it.

In Dart programming there is no difference, it is same.

But in Flutter specifically it is used mostly with widgets, to optimize the performance of the application.

Flutter app is created with combining widgets, almost 95% of app is made with widgets.
It will contains full tree of widgets.

If we are using any stateful widgets or any animation that needs to change again and again, automatically or with user interaction.

Every state change will trigger app to refresh that means the widgets which is changed that and its child widgets get rebuilt again or
Flutter will re-paint the UI again.

There might be children widgets that no need to rebuilt again, we can just rebuilt the widgets which actually changed and not all.

Internally in device where we are using the application, Garbage collector needs to work more, unnecessary widget rebuilt means garbage collector needs to remove the instance of widget from memory and also memory needs to store duplicate instance of same element if we are reusing that widget in any other location in app.

To avoid this we use const in front of those widgets which developers think will not change after re-render. That will make sure that Flutter will only re-render the widgets that needs to be, the const widgets will not re-render after the refresh.

## Scaffold widget

It implements the basic structure of app, basic design.
`body` named argument needs to pass to show other widgets on top of scaffold.
For ex -

```dart
Scaffold(
    body: Text("Hello World!");
)
```

Scaffold widget in detail or more basic widgets: https://docs.flutter.dev/ui/widgets/basics

## Text widget

It shows any string on app.
positional argument string required.

```dart
Text("Hello World!");
```

Text widget in detail or more basic widgets: https://docs.flutter.dev/ui/widgets/basics

## Center widget

It is used to center the widgets.
`child` named argument required.

```dart
Center(
    child: Text("Hello World!"),
)
```

Center widget in detail or more layout widgets: https://docs.flutter.dev/ui/widgets/layout

## Custom Stateless Widget

Custom stateless widget is created by defining class and inheriting stateless widget which is provided by Flutter.

```dart
// Syntax ->

class YourCustomWidgetClassName extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return // widget tree..
    }
}
```

`StatelessWidget` is a class provided by Flutter to create our own Stateless Widget.
`@override` is a annotation used to let Flutter know that we are overriding function defination from StatelessWidget to our own function defination of the same function name.
`build()` method Flutter executes by itself when you call your own custom widget constructor function into your widget tree. It will automatically call by Flutter and return your custom Widget tree which you want to return.

For ex -

```dart
class GradientContainer extends StatelessWidget {

    @override
    Widget build(BuildContext context) {
        return Container(
          decoration: const BoxDecoration(
            gradient: LinearGradient(
              colors: [Colors.blueAccent, Colors.deepPurple],
              begin: Alignment.topLeft,
              end: Alignment.bottomRight,
            ),
          ),
          child: const Center(
            child: Text(
              "Hello World!!!",
              style: TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
                fontSize: 30.0,
              ),
            ),
          ),
        ),
    }
}

// use your custom widget into your widget tree.

runApp(
    MaterialApp(
      home: Scaffold(
        body: GradientContainer(), // when you call your custom widget, Flutter automatically calls build method defined inside your custom widget.
      ),
    ),
  );
```

Note - If you define custom widget by creating class like above, you will receive one warning like "Constructors for public widgets should have a named 'key' parameter."

This warning comes because, you need to forward `key` named argument to parent class here in this case `StatelessWidget` class.
For this you need to create first constructor function inside our custom class then calls `super()` function which will forward `key` when you pass argument `key` to `super()` function.

Constructor function can be created with the same name of class + adding parenthesis and a function body like a normal function.

```dart
class YourCustomWidgetName extends StatelessWidget {
    // Named argument can be written inside {} in dart.
    YourCustomWidgetName({/*accept named argument for ex - key*/}) {
        // some initialization..
    }
}
```

If you don't want to do any initialization and normally just want to resolve that warning and just want to create basic constructor function, it can be created like below.

```dart
class YourCustomWidgetName extends StatelessWidget {
    const YourCustomWidgetName({key}): super(key: key) // forwarding "key" which we are accepting in our custom widget to "key" named argument of super function. This "key" which we are receiving inside our custom widget is passed by Flutter itself, while calling our constructor function of our custom widget.
}
```

Shortcut for forwarding key, provided by dart is

```dart
class YourCustomWidgetName extends StatelessWidget {
    const YourCustomWidgetName({super.key}) // This shortcut will do both, it will accept and forward the "key" to parent's constructor function.
}
```

For ex -

```dart
class GradientContainer extends StatelessWidget {

    const GradientConstainer({super.key});

    @override
    Widget build(BuildContext context) {
        return Container(
          decoration: const BoxDecoration(
            gradient: LinearGradient(
              colors: [Colors.blueAccent, Colors.deepPurple],
              begin: Alignment.topLeft,
              end: Alignment.bottomRight,
            ),
          ),
          child: const Center(
            child: Text(
              "Hello World!!!",
              style: TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
                fontSize: 30.0,
              ),
            ),
          ),
        ),
    }
}
```
