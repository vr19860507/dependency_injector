# dependency_injector

A dependency injection system for Flutter that automatically calls a dispose method if there is one.

## Getting Started

Documentation coming soon.
API for writing tests coming soon.
For now you can look at the source code of the [example](https://pub.dev/packages/dependency_injector/example) and run it.

Basic example

```dart
import 'package:flutter/material.dart';
import 'package:dependency_injector/dependency_injector.dart';

class SomeService {
  final Repository repository = inject();
}

class Repository {
  String getData() => 'Hello world.';
}

final services = [
  Transient(() => SomeService()),
  Singleton(() => Repository()),
];

void main() {
  runApp(RootInjector(
    services: services,
    child: Injector(() => MyApp()),
  ));
}

class MyApp extends StatelessWidget {
  MyApp({Key key}) : super(key: key);

  final SomeService someService = inject();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: Scaffold(
        body: Center(child: Text(someService.repository.getData())),
      ),
    );
  }
}
```