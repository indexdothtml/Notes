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
Flutter by default looks for `lib/main.dart` file name under lib folder, to check main function inside that file, but if doesn't find main.dart file then it gives error.
If you want to use different file name then you need to tell flutter where to look it, by default it won't look in all files for main function.
For ex - `flutter run -t lib/my_file.dart`

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

`main` function is not a built-in function, but still flutter compiler will look for this function when you run your app, it is like hardcoded in flutter compiler to look for this function to start executing the app.

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

## variables in Dart

Variables can be created by `var` keyword in dart.

For ex -

```dart
var greetingsVariable = "Hello";
```

Dart can infer the type of variable from the initial value.

NOTE: In dart without initialization of variable, it will consider `null` as a default value.

with `var` keyword it is possible to declare variable without initialization.

```dart
var greetingsVariable;

print(greetingsVariable) // null
```

In dart variables can be declared with specific type assign to it.

For ex -

```dart
int favNumber = 6;
String text = "Hey";
```

But can't be unintialized like `var`. If required to intialize later then make it optional using '?' chracter after type

```dart
// This is not allowed
int favNumber;
String text;

// Make it optional
int? favNumber; // this can be either int or null
String? text; // this can be either String or null
```

Variables can be unchangable after first initialization, with the help of `const` and `final`

Difference ->

If you know the initial value is fixed, and can be available at compile time then use `const`.

```dart
// When below line run at compile time, value is already available.
const creator = "Abhishek";
//or
const String creator2 = "Abhishek"; // spcifically defining type as well.
```

If you know the initial value is fixed, but don't know at compile time, instead it is going to be generate at runtime then use `final`

```dart
int generateUniqueID() {
  // generating unique id
}

// When below line run at compile time, value is not available at that moment, when function will run at runtime at that moment it will generate value and assign it to the variable, but after that at any point of time in code if we try to change variable value it won't accept new value.
// If value of constant not known at compile time and only known at runtime then 'final' will be used instead of 'const'.
final generateID = generateUniqueID();
// or
final int generateID = generateUniqueID() // specifing type here can be useful then const because it gives some type safty so it will not store any other value then int at runtime for this example.
```

If value value don't know already, but type is known and variable is not going to change further in code then

```dart
final String name;
```

## Instance variables or Properties in classes.

It is possible to accept arguments in custom created widgets.

For ex -

```dart
class StyledText extends StatelessWidget {
  const StyledText(this.text, {super.key});

  final String text;

  @override
  Widget build(BuildContext context) {
    return Text(
      text,
      style: const TextStyle(
        color: Colors.white,
        fontWeight: FontWeight.bold,
        fontSize: 30.0,
      ),
    );
  }
}
```

In above code, arguments are accepted by defining parameter name inside constructor function with `this` keyword.

In above code, we are accepting positional argument called "text" (which is `required` by default) but you can accept named argument as well inside {} brackets (named arguments are `optional` by default)

The line `final String text;` is a property of class or instance variable, without it all methods inside class will not have access of "text" variable.

Although "text" variable is also inside constructor function but, constructor function and other methods inside class are not connected and shares variable automatically, to happen that, properties must need to define.

Normally without `this` keyword you can accept argument like below but you have to manually assign the value to property.
Because it is very common to accept arguments, Dart given shortcut with `this` keyword.

For ex -

```dart
class StyledText extends StatelessWidget {
  const StyledText(String text, {super.key}): outText = text;

  final String outText;

  @override
  Widget build(BuildContext context) {
    return Text(
      outText,
      style: const TextStyle(
        color: Colors.white,
        fontWeight: FontWeight.bold,
        fontSize: 30.0,
      ),
    );
  }
}
```

## Constructor function and adding multiple constructor function

Constructor functions as we saw above, it is declared inside class so we can use that class, it creates the object of that class.

For ex - Below `const StyledText(...)` is a constructor function.

```dart
class StyledText extends StatelessWidget {
  const StyledText(String text, {super.key}): outText = text;

  final String outText;

  @override
  Widget build(BuildContext context) {
    return Text(
      outText,
      style: const TextStyle(
        color: Colors.white,
        fontWeight: FontWeight.bold,
        fontSize: 30.0,
      ),
    );
  }
}
```

But you can add more than one constructor function. With ClassName.anotherConstructorFunctionName()

For ex -

```dart
class StyledText extends StatelessWidget {
  const StyledText(String text, {super.key}) : outText = text;

  const StyledText.helloWorld({super.key}) : outText = "Hello World!";

  final String outText;

  @override
  Widget build(BuildContext context) {
    return Text(
      outText,
      style: const TextStyle(
        color: Colors.white,
        fontWeight: FontWeight.bold,
        fontSize: 30.0,
      ),
    );
  }
}
```

So you can use above StyledText Widget like

```dart
StyledText.helloWorld();
```

## How to add static images in your Flutter project

1. Create a folder named "assets" though name can be anything but "assets" is convention.

2. Move all your images into "assets/images" folder.

3. In pubspec.yaml file uncomment the "assets:" line which can be look like this

```yaml
# To add assets to your application, add an assets section, like this:
# assets:
#   - images/a_dot_burr.jpeg
#   - images/a_dot_ham.jpeg
```

4. Add your images after "assets:" with 1 tab space and "-" symbol before your file path. Important to note here is path to the image file should be relative path and not absolute path, so it should be relative to pubspec.yaml file

5. For ex -

```yaml
# To add assets to your application, add an assets section, like this:
assets:
  - assets/images/image_name1.jpeg
  - assets/images/image_name2.jpeg
  - assets/images/image_name3.jpeg
```

You can add images in your project simply with `Image()` widget provided by Flutter.

```dart
Image(image: /*image provider widget*/) // NOTE: add example for this
```

If you have images already in your project suppose in "assets" folder then you can just use another constructor provided by the `Image()` widget called `asset` constructor

For ex -

```dart
Image.asset('assets/images/image_name1.jpeg');
```

## Buttons in Flutter

Buttons are common in application so, Flutter provides some already built in Button widgets with different styling and some with different functionality.

Most of the accept two arguments minimum like "onPressed" which require function as a argument and "text" which require Text widget normally to show button text.

Some of the Button widgets require "icon" instead of "text" argument and need "Icon" widget to pass. like "IconButton" widget.

Some of them require only "onPressed" widget at minimum not other argument like "FloatingActionButton" widget.

You can see in detail all the Buttons and use of it here: https://docs.flutter.dev/get-started/fundamentals/user-input

One example -

```dart
handleOnPress() {
  // do something when user pressed this button
}

TextButton(onPressed: handleOnPress, text: Text('Click here')); // Just pass function reference, don't execute when onPressed event will trigger it will automatically find function with the reference you passed and execute it.

//Another way
TextButton(onPressed: () { /*your logic*/}, Text('Click here')); // () {} this is anonymous function. But it can't be reused.

```

## Row and Column widget in Flutter

Column widget if you have multiple childrens and want to display it vertically one after another.

A widget that displays its children in a vertical array.

To cause a child to expand to fill the available vertical space, wrap the child in an Expanded widget.

The Column widget does not scroll (and in general it is considered an error to have more children in a Column than will fit in the available room). If you have a line of widgets and want them to be able to scroll if there is insufficient room, consider using a ListView.

More information - https://api.flutter.dev/flutter/widgets/Column-class.html?_gl=1*uu9h3z*_ga*MTAzMjcyNjA3MC4xNzQ5NzQ4ODA4*_ga_04YGWK0175*czE3NDk3NDg4MDgkbzEkZzEkdDE3NDk3NTAyNDIkajYwJGwwJGgw

Row widget if you have multiple childrens and want to display it horizontally one after another.

A widget that displays its children in a horizontal array.

To cause a child to expand to fill the available horizontal space, wrap the child in an Expanded widget.

The Row widget does not scroll (and in general it is considered an error to have more children in a Row than will fit in the available room). If you have a line of widgets and want them to be able to scroll if there is insufficient room, consider using a ListView.

More information - https://api.flutter.dev/flutter/widgets/Row-class.html?_gl=1*j0mroq*_ga*MTAzMjcyNjA3MC4xNzQ5NzQ4ODA4*_ga_04YGWK0175*czE3NDk3NDg4MDgkbzEkZzEkdDE3NDk3NTAxOTEkajE4JGwwJGgw

NOTE - Column widget will take full space on its main axis which is on Column (vertically), So Column widget by default takes full height.
Row widget on other hand take full space on its main axis which is on Row (horizontally), So Row widget by default takes full width.

You can alter this behaviour with `mainAxisSize` property in Column or Row widget, you can set `mainAxisSize: MainAxisSize.min` to take minimum height or width how much its children wants. By default it is set to `MainAxisSize.max`.

## Styling TextButton widget

You can override the default styling of the `TextButton` widget with the passing `style` argument to it.

Easiest way to create style for `TextButton` widget is to call `styleFrom()` constructor from same `TextButton` widget and `styleFrom()` constructor function contains all the styles which you can apply to override the default style TextButton widget.

```dart
TextButton(
  onPressed: rollDice,
  style: TextButton.styleFrom(
    foregroundColor: Colors.white,
    textStyle: const TextStyle(fontSize: 20),
    // padding: const EdgeInsets.only(top: 20),
  ),
  child: const Text("Roll Dice"),
),
```

## Column spacing in Column widget

There are different ways you can add spacing.

1. `padding` - with padding inside `style` argument you can add spacing between two childrens

For ex -

```dart
TextButton(
  onPressed: rollDice,
  style: TextButton.styleFrom(
    foregroundColor: Colors.white,
    textStyle: const TextStyle(fontSize: 20),
    padding: const EdgeInsets.only(top: 20), // add only 20px on 'top' there are more arguments like 'bottom', 'left', 'right'.
    //padding: const EdgeInsets.all(20), // you can add in all direction.
  ),
  child: const Text("Roll Dice"),
),
```

2. `SizedBox()` widget - It will help to add widget specifically Box with some width, height and child if you want to give, default it will not have anything no width, height and child, it will not visible on screen as well, developers define how it looks.

`SizedBox()` widget not change its width or height with its content inside children like container, `SizedBox()` takes fix size which we give it to it, overflow content just get cut out.

You can add space vertically with giving `height` argument to it.

```dart
Column(
  mainAxisSize: MainAxisSize.min,
  children: [
    Image.asset('assets/images/dice-2.png', width: 200),
    const SizedBox(height: 20), // SizedBox for vertical spacing.
    TextButton(
      onPressed: rollDice,
      style: TextButton.styleFrom(
        foregroundColor: Colors.white,
        textStyle: const TextStyle(fontSize: 20),
        // padding: const EdgeInsets.only(top: 20),
        // padding: const EdgeInsets.all(20)
      ),
      child: const Text("Roll Dice"),
    ),
  ],
),
```

3. More will come... :)

## StatefulWidget in Flutter

There are two types of custom widget you can create `StatelessWidget` and `StatefulWidget`.

When to use which:

Whenever you have any changing value in widget, which can trigger change in UI, that time `StatefulWidget` is used.

Whenever you don't have such things and your widgets just accepting arguments or not accepting any arguments also then `StatelessWidget` is used.

How to create StatefulWidget:

Normally whenever State inside the StatefulWidget changes, the `build` method in widget where state got changed and its all children widget's `build` method gets executed again that means re-build, which cause re-rendering of those widgets only which build method got called.

Or in simple terms, the state in which widget gets updated, that widget and that widget's subtree gets re-rendered.

StatefulWidget have to create seperatly in another file so it won't cause problem with other stateless widget and unwanted re-renders.
Also StatefulWidget needs to be splitted in two classes, first which creates StatefulWidget with extending StatefulWidget and another class which creates State of that widget which extends State object.

```dart
import 'package:flutter/material.dart';

class DiceRoller extends StatefulWidget {
  const DiceRoller({super.key});

  // Instead of build method stateful widget force to implement createState method.
  @override
  State<DiceRoller> createState() {
    return _DiceRollerState();
  }
}

// The class name starting with _ (underscore) is private class.
// Private class only be available inside same file where it is declared.
// State generic object creates the state class which can be used inside our StatefulWidget class.
class _DiceRollerState extends State<DiceRoller> {
  var activeDiceImage = 'assets/images/dice-2.png';

  rollDice() {
    // setState method provided by State class, call build method of same class where it is used and its subtree widget's build method. Which cause re-rendering of those widgets.
    setState(() {
      activeDiceImage = 'assets/images/dice-4.png';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      children: [
        Image.asset(activeDiceImage, width: 200),
        const SizedBox(height: 20),
        TextButton(
          onPressed: rollDice,
          style: TextButton.styleFrom(
            foregroundColor: Colors.white,
            textStyle: const TextStyle(fontSize: 20),
            // padding: const EdgeInsets.only(top: 20),
            // padding: const EdgeInsets.all(20)
          ),
          child: const Text("Roll Dice"),
        ),
      ],
    );
  }
}
```

## StatelessWidget Vs StatefulWidget

1. StatelessWidget does not store any states, it gets rendered once and never change at runtime, unless parent widget changes.
   It does not change after it defined once.
2. StatefulWidget does store states, and whenever state changes with `setState` method, build method gets called and UI gets updated. It does change at runtime, if state get updated, to show updated date in UI.

## Flutter Stateful widget lifecycle

Every Flutter Widget has a built-in lifecycle: A collection of methods that are automatically executed by Flutter (at certain points of time).

There are three extremely important (stateful) widget lifecycle methods you should be aware of:

1. initState(): Executed by Flutter when the StatefulWidget's State object is initialized

2. build(): Executed by Flutter when the Widget is built for the first time AND after setState() was called

3. dispose(): Executed by Flutter right before the Widget will be deleted (e.g., because it was displayed conditionally)

## initState() method in Flutter

`initState()` which can be available inside State class, it will only execute once when state object initialize in stateful widget.
It is used to do some initialization.

For ex - here we are initializing activeScreen variable first time when object executes passing function reference to that widget.

```dart
class Quiz extends StatefulWidget {
  const Quiz({super.key});

  @override
  State<Quiz> createState() {
    return _QuizState();
  }
}

class _QuizState extends State<Quiz> {
  Widget? activeScreen;

  @override
  void initState() {
    super.initState();
    activeScreen = StartScreen(switchScreen);
  }

  void switchScreen() {
    setState(() {
      activeScreen = const QuestionsScreen();
    });
  }

  //.....
  //......
}
```

## double.infinity in Flutter

In Dart `double.infinity` value constant can provide infinite value, the implementation is like `1.0/0.0`.

Usecase of this can be taking height or/and width as much as possible or available.

For ex -

```dart
SizedBox(
  height: 300,
  width: double.infinity, // takes full available width of the screen.
)
```

More info - https://stackoverflow.com/questions/61706455/whats-the-difference-between-double-infinity-and-double-maxfinite-in-dart
