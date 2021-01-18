# demo-flutter-web
Demo flutter app for web and mobile



1. Task - Create a demo app (mobile + web) --> starter Flutter app (counter, button and blue appBar) 

Firstly create app as:

	flutter create demo_flutter_web

When we create an app like this, like the ZeljoApp is created we can not run this app immediately in web it only can be run on mobile or mobile emulator, so, we need to add web support in to existing app.

For adding web suport we need change channel of flutter:

	flutter channel master

When we are on master channel of app we can than add web support:

	flutter config --enable-web

With this we are enabling app to be on web, it takes a little bit of time to download everything needed and after that we need web folder in our app, like android and ios.

For that we have command:

	flutter create .

But the problem we are facing is that we can not do this command because of lockfile in flutter, so we need to delete "Program file\Flutter\bin\cache\lockfile" after that we can again do: 

	flutter create .

Than we need to open this app in web with:

	flutter devices

Which shows us which devices are available, like chrome, than we run app on chrome with other command:

	flutter run -d chrome

We can two app running at the same time on mobile and on chrome.



2. Task - Make changes on the web app, but mobile shouldn't change (button should be removed on the web version, but mobile will be the same as starter project)

We can add import as:

	import 'package:flutter/foundation.dart' show kIsWeb;

kIsWeb is global bool variable which is true when 0 and 0.00 is equal, which in javascript are, but not in dart, so when app is run on mobile kIsWeb will be false because 0 and 0.00 are not equal.

if we want to remove button on web we can do it as this snippet od code:

	floatingActionButton: !kIsWeb ?  FloatingActionButton(
        		onPressed: _incrementCounter,
        		tooltip: 'Increment',
        		child: Icon(Icons.add),
      		) : Container()



3. Task - Create a layout change on the web app without affecting the mobile side. (i.e. Mobile AppBar should hold the blue color, while on the web, AppBar should be different color, and also margin on the web, should be different from the mobile side.

In this task we need to change color of theme, again with using kIsWeb we can do it with this snippet od code:

	theme: ThemeData(
        	primarySwatch: !kIsWeb ? Colors.blue : Colors.orange,
        	visualDensity: VisualDensity.adaptivePlatformDensity,
      	      )

To change margin we can again do it with kIsWeb:

	appBar: AppBar(
        		title: kIsWeb ? Center(child: Text(widget.title)) : Text(widget.title),
      		)
		
		

# ZeljoDostavaApp

Mobile and web app

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

## Getting Started with Flutter web

This project was firstly made for android and then it needed to have web also

First of all we needed to enable web for this app:

    flutter congif --enable-web

We also need web folder which is used for web app, we create it with:

    flutter create .

There is problem which we had, package name is not supported by Dart which is ZeljoDostavaApp, it needs to have only lowcase letter and underlines, more can be read on [online documentation](https://dart.dev/guides/packages)

We changed it to zeljo_dostava

We can run program then with:

    flutter run -d chrome

This lead us to another problem where we have two package name: at.zeljo and com.example, so we changed it in whole project to be at.zeljo

When we run our app on web now it works but immedieately crashes because we can not use: 

    Platform.isIOS

All places in code where we used it are now like this

    if(!kIsWeb){
        Platform.isIos ? ...
    }

This kIsWeb is true when we are on web version of this app so Platform.isIOS will never be reached on web.

## Login screen

Next problem we have is on login screen where when can not add phone.

The solution is that instead of using 

    verifyPhoneNumber() 
    
we must use:

    signInWithPhoneNumber()

After that we have new problem which is that in verification function there is not verifiationID.

This can be solved by adding [then] after [signInWithPhoneNumber()] like:

    signInWithPhoneNumber().then((value) => verificationID = value);

After that change we can succesfully go through to NewsFeed screen.

We also have problem with Facebook and Google login

For google login we need to add meta tag in index.html file in web folder:

    <meta name="google-signin-client_id" content="575024045364-3tos4oqc1fh8r807n7sl1fdbh08c5j50.apps.googleusercontent.com">

After which we have error in console when I started web app in Google Chrome:

    Uncaught (in promise) Error: PlatformException(idpiframe_initialization_failed, Not a valid origin for the client: http://localhost:58248 has not been whitelisted for client ID 575024045364-3tos4oqc1fh8r807n7sl1fdbh08c5j50.apps.googleusercontent.com. Please go to https://console.developers.google.com/ and whitelist this origin for your project's client ID., https://developers.google.com/identity/sign-in/web/reference#error_codes, null)

After which i installed mozilla firefox, and created new web app on console.developers.google.com

    Zeljo Dostava

with Client ID:

    575024045364-0eqtp57cfnjlj7qn9lajbns1hs4fl8ak.apps.googleusercontent.com

and that client id I added in meta in index.html. After I restarted application, and run it mozilla firefox it worked.

I tried again with Google and it worked there also.

## News feed screen

On news feed we have problem where we can not use AppSignInWithIphone provider because this provider uses IphoneSignInAvailable which is similar to Platform.isIOS thus we will put it like:

    if(!kIsWeb){
        Provider<IphoneSignInAvailable>....
    }





















# ZeljoDostavaApp

Mobile and web app made in Flutter

## Getting Started with Flutter web

This is a project made in Flutter which was firstly made for Android and iOS and we need to add web support to it.

First thing we need to do is to change channel of flutter to master because only with master channel we can add web support for the existing project in flutter.
We can do that with terminal command:

    flutter channel master

_please note that you are required to be in app's directory in terminal_

After we switched channels we are ready to add web support in existing Flutter project.
We can do that with terminal command:

    flutter congif --enable-web

Till now, we only enabled web support in this project, we still do not have web folder in it.
For that matter, we can create web folder in this project with command:

    flutter create .

After this command we encountered a problem.

    ZeljoDostavaApp package name is not supported by Dart

This problem indicates us that we have incorrect name of package.
Dart package name can only be composed from lowcase letters and underlines.
_more about this can be read on [online documentation](https://dart.dev/guides/packages)_

We must change it to so zeljo_dostava. The places where it must be changed are: 

In pubspec.yaml

Instead of:

    name: ZeljoDostavaApp
    description: A new Flutter project.

We write:

    name: zeljo_dostava
    description: A new Flutter project.

We also must change a name of the folder in which is whole project stored from:

    ZeljoDostavaApp

to: 

    zeljodostava

_if the directory of project was C://Desktop/ZeljoDostavaApp now it must be C://Desktop/zeljodostava_

Also in projects's __AndroidManifest.xml__ we must change package name like:

<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="at.zeljo.zeljo_dostava">

In __build.gradle__ inside of app folder it must go like:

    defaultConfig {
    applicationId "at.zeljo.zeljo_dostava"
    minSdkVersion 16
    targetSdkVersion 27

We must do one more directory change for MainActivity.kt file from: 

    android\app\src\main\java\com\example\ZeljoDostavaApp

to:

    android\app\src\main\java\at\zeljo\zeljo_dostava

---

After all these changes we can again build web with terminal command:

    flutter build web

And after build we can run web app with command:

    flutter run -d chrome

When we run our app on web now it works but immedieately crashes after splashscreen because we can not use: 

    Platform.isIOS

Even though this line of code should work because sometimes for web we can use this line of code:

    Platform.isMacOS

Which tells us if the app is running on macOS, _Platform.is_ is still not supported by Flutter web.

Instead of using Platform.isWindows we can use _kIsWeb_. We need to add import as: 

    import 'package:flutter/foundation.dart' show kIsWeb;

_kIsWeb_ is global bool variable which is true when 0 and 0.00 is equal, which in javascript are, but not in dart, so when app is run on mobile kIsWeb will be false because 0 and 0.00 are not equal.

All places in code where we used it are now like this

    if(!kIsWeb){
        Platform.isIos ? ...
    }

This kIsWeb is true when we are on web version of this app so Platform.isIOS will never be reached on web.

For example when we need to show something on web but not on android and IOs we can do it as:
'''dart
    floatingActionButton: !kIsWeb ?  FloatingActionButton(
    		onPressed: _incrementCounter,
    		tooltip: 'Increment',
    		child: Icon(Icons.add),
  		) : Container()

## Login screen

Next problem we have is on login screen where when can not add phone.

The solution is that instead of using 

    verifyPhoneNumber() 
    
we must use:

    signInWithPhoneNumber()

After that we have new problem which is that in verification function there is not verifiationID.

This can be solved by adding [then] after [signInWithPhoneNumber()] like:

    signInWithPhoneNumber().then((value) => verificationID = value);

After that change we can succesfully go through to NewsFeed screen.

We also have problem with Facebook and Google login

For google login we need to add meta tag in index.html file in web folder:

    <meta name="google-signin-client_id" content="575024045364-3tos4oqc1fh8r807n7sl1fdbh08c5j50.apps.googleusercontent.com">

After which we have error in console when I started web app in Google Chrome:

    Uncaught (in promise) Error: PlatformException(idpiframe_initialization_failed, Not a valid origin for the client: http://localhost:58248 has not been whitelisted for client ID 575024045364-3tos4oqc1fh8r807n7sl1fdbh08c5j50.apps.googleusercontent.com. Please go to https://console.developers.google.com/ and whitelist this origin for your project's client ID., https://developers.google.com/identity/sign-in/web/reference#error_codes, null)

After which i installed mozilla firefox, and created new web app on console.developers.google.com

    Zeljo Dostava

with Client ID:

    575024045364-0eqtp57cfnjlj7qn9lajbns1hs4fl8ak.apps.googleusercontent.com

and that client id I added in meta in index.html. After I restarted application, and run it mozilla firefox it worked.

I tried again with Google and it worked there also.

## News feed screen

On news feed we have problem where we can not use AppSignInWithIphone provider because this provider uses IphoneSignInAvailable which is similar to Platform.isIOS thus we will put it like:

    if(!kIsWeb){
        Provider<IphoneSignInAvailable>....
    }




