# Introduction

1) First goto your pubspec.yaml file and add dependency:
   ```
   flutternetworkservicehandler:
   ```
2) run flutter pub get to update the packages dependencies.

3) In your code, you can use it like this:
  first import the package:
  ```
 import 'package:flutternetworkservicehandler/HttpNetworkService.dart';
  ```
# Code Usage
then use it like this in your code:
  ```

import 'package:flutter/material.dart';
import 'package:flutternetworkservicehandler/HttpNetworkService.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  List _usersList = [];

  Future getUsersData() async {
    try {
      final responseUsersList = await HttpNetworkService.getRequest(
          url: 'https://jsonplaceholder.typicode.com/users',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
          });
      for (var items in responseUsersList) {
        print(items);
        _usersList.add({
          'id': items['id'],
          'username': items['username'],
          'website': items['website'],
        });
      }
    } catch (e) {
      print(e.toString());
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: FutureBuilder(
        future: getUsersData(),
        builder: (ctx, snapshot) =>
            snapshot.connectionState == ConnectionState.waiting
                ? Center(
                    child: CircularProgressIndicator(),
                  )
                : ListView.builder(
                    itemCount: _usersList.length,
                    itemBuilder: (ctx, i) => ListTile(
                      title: Text(_usersList[i]['username']),
                      subtitle: Text(_usersList[i]['website']),
                      leading: CircleAvatar(
                        child: FittedBox(
                          child: Text(
                            _usersList[i]['id'].toString(),
                          ),
                        ),
                      ),
                      trailing: Icon(
                        Icons.arrow_forward_ios,
                      ),
                    ),
                  ),
      ),
    );
  }
}
```

# SUPPORT
You liked this package? then give it a star. If you want to help then:
Star this repository.
Send a Pull Request with new features, see Contribution Guidelines.
Share this package.
Create issues if you find a Bug or want to suggest something.

