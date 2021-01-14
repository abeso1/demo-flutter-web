# demo-flutter-web
Demo flutter app for web and mobile
Task 1. Create a demo app (mobile + web) --> starter Flutter app (counter, button and blue appBar) 
 - i made app with 
		flutter create demo_flutter_web
 	When we create an app like this, like the ZeljoApp is created we can not run this app immediately in web
	it only can be run on mobile or mobile emulator
        So, we need to add web support in to existing app
 - for adding web suport we need change channel of flutter
		flutter channel master
	When we are on master channel of app we can than add web support
		flutter config --enable-web
	with this we are enabling app to be on web, it takes a littble bit of time to download everything needed
	and to setup app for web, but we still need one thing
	We need web folder in our app, just like android and ios
- for that we have command
		flutter create .
	but the problem we are facing is that we can not do this command because of lockfile in flutter,
	so we need to delete Program file\Flutter\bin\cache\lockfile
	after that we can again fo flutter create .
	than we need to open this app in web
- for that we have two commands
		flutter devices
	it shows us which devices are available, like chrome
	than we run app on chrome with other command
		flutter run -d chrome
- we can two app running at the same time on mobile and on chrome