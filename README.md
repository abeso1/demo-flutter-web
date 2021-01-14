# demo-flutter-web
Demo flutter app for web and mobile

- Task 1. Create a demo app (mobile + web) --> starter Flutter app (counter, button and blue appBar) 
 1. I made app with 
		- flutter create demo_flutter_web
 	- When we create an app like this, like the ZeljoApp is created we can not run this app immediately in web
	- it only can be run on mobile or mobile emulator
        - So, we need to add web support in to existing app
 2. for adding web suport we need change channel of flutter
		- flutter channel master
	- When we are on master channel of app we can than add web support
		- flutter config --enable-web
	- with this we are enabling app to be on web, it takes a littble bit of time to download everything needed
	- and to setup app for web, but we still need one thing
	- We need web folder in our app, just like android and ios
 3. for that we have command
		- flutter create .
	- but the problem we are facing is that we can not do this command because of lockfile in flutter,
	- so we need to delete Program file\Flutter\bin\cache\lockfile
	- after that we can again fo flutter create .
	- than we need to open this app in web
 4. for that we have two commands
		- flutter devices
	- it shows us which devices are available, like chrome
	- than we run app on chrome with other command
		- flutter run -d chrome
 5. we can two app running at the same time on mobile and on chrome

- Task 2. Make changes on the web app, but mobile shouldn't change (button should be removed on the web version, but mobile will be the same as starter project)
 1. we can add import as
		- import 'package:flutter/foundation.dart' show kIsWeb;
	- this kIsWeb is global bool variable which is true when 0 and 0.00 is equal, which in javascript are, but not in dart
	- so when app is run on mobile kIsWeb will be false because 0 and 0.00 are not equal
 2. if we want to remove button on web we can do it as this snippet od code
		- floatingActionButton: !kIsWeb ?  FloatingActionButton(
        		onPressed: _incrementCounter,
        		tooltip: 'Increment',
        		child: Icon(Icons.add),
      		) : Container(),

- Task 3. Create a layout change on the web app without affecting the mobile side. (i.e. Mobile AppBar should hold the blue color, while on the web, AppBar should be different color, and also margin on the web, should be different from the mobile side.
 1. so in this task we need to change color of theme, again with using kIsWeb we can do it with this snippet od code
	      - theme: ThemeData(
        	primarySwatch: !kIsWeb ? Colors.blue : Colors.orange,
        	visualDensity: VisualDensity.adaptivePlatformDensity,
      	      ),
 2. to change margin we can again do it with kIsWeb
	      - appBar: AppBar(
        		title: kIsWeb ? Center(child: Text(widget.title)) : Text(widget.title),
      		),
		
		