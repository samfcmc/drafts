React Native
=========================

# Introduction
Developing mobile apps for multiple platforms can imply an huge effort since each platform has its own APIs and tools.
If we want our apps to reach a good portion of the market we end up developing for Android and iOS. Instead of having just one team we have at least two, one for each platform.

Instead of using the native APIs we can use alternative solution such as hybrid frameworks like [ionic](http://ionicframework.com/) allowing us to write apps using web technologies such as HTML, CSS and JS. The framework generate packages which we can upload to [Play Store](https://play.google.com) and [App Store](https://itunes.apple.com).
Why developers write native apps instead of hybrid?
The idea of having only one code base for multiple platforms seems appealing.
However, each platform has its own characteristics. Users of each one expect different things.
Also, performance is an issue in hybrid apps.
This is why most apps are still native.
Mark Zuckerberg said: ["Our Biggest Mistake Was Betting Too Much On HTML5"](http://techcrunch.com/2012/09/11/mark-zuckerberg-our-biggest-mistake-with-mobile-was-betting-too-much-on-html5/).

What if we could have the best of native and hybrid?
An user interface designed for each platform and one code base that can work on both platforms?
[React native](https://facebook.github.io) is a framework created by Facebook which allows to develop mobile apps using web technologies but the UI is designed specifically for each platform (iOS and Android).
It was built on top of [ReactJS](https://facebook.github.io/react/).


# Requirements
In order to use `react-native` you will need the following:
* [NodeJS](https://nodejs.org) and [NPM](https://www.npmjs.com)
* Android SDK to be able to run the Android version
* XCode to be able to run the iOS version

# Get started
If you already installed `node` and `npm` you need to install `react-native-cli`, which provides a command line tool to create and manage projects.
Install it:
```shell
npm install -g react-native-cli
```

Then, create your project:
```shell
react-native init MyProject --verbose
```

Note: I advise you to run with `--verbose` option because this command takes a long time and you can see what is going on before killing it because you think it is frozen.

Congratulations, you created your first react native project.

As you can see your newly created project have the following structure
```shell
MyProject
|-- android
|   |-- ...
|-- ios
|   |-- ...
|-- package.json
|-- index.ios.js
|-- index.android.js
```

Inside `android` and `ios` folders you have an Android and iOS projects which you can open with [Android Studio]() and [XCode](), respectively.
If you still need to write native code you can. You can even call that native code in your react code. See the links below:
* [Native Modules (iOS)](https://facebook.github.io/react-native/docs/native-modules-ios.html#content)
* [Native Modules (Android)](https://facebook.github.io/react-native/docs/native-modules-android.html#content)

You can start by looking at `index.ios.js` and `index.android.js` files.
These files are the starting point of your app.

If you look at the `index.android.js` you will see the following:
```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 */
'use strict';

var React = require('react-native');
var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
} = React;

var MyProject = React.createClass({
  render: function() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.android.js
        </Text>
        <Text style={styles.instructions}>
          Shake or press menu button for dev menu
        </Text>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

AppRegistry.registerComponent('MyProject', () => MyProject);
```

If you never worked with ReactJS you should be looking at the file like "WTF":

![wtf](http://i.imgur.com/M4iIlOy.jpg)

This is a special syntax that `React` uses which is `JSX`. Don't worry about how to compile this syntax to `Javascript`. React native will handle it for you.

Now that you know the basics, it is time to run your project on an emulator or device.

# Running in Android
You can use an Android device or an emulator.
However, you first need to define and `ANDROID_HOME` environment variable that points to Android Studio root directory on your computer.
Turn on your emulator or connect your device through an USB cable.
Then, run the following command:
```shell
react-native run-android
```

And voilla. Your app is running on your emulator or device.

Don't worry if this command doesn't run successfully and return some errors.
It happened to me the first time I tried.
I was having some errors because I didn't have the `Build tools` version 23.0.1 and `API 23` installed.
The error message will give you hints about what is missing.
To fix this, open the `Android SDK manager and` and install all the missing packages.

After you managed to run the app on your emulator or device you can start making changes to your `index.android.js` file.

## Using a real device
If you are using a real device you can have live reloading of your changes.
First, you need to configure your app to connect to the debug server that you launched with `run-android` command.

Connect your device to your computer through USB, open your MyProject app on your device and run:
```shell
adb reverse tcp:8081 tcp:8081
```

Note: if you don't have `adb` command available you must add `<Android SDK path>/platform-tools` to your `PATH` environment variable.

Now, without closing the app on your device open the Developer options.

To do that you need to press the menu button on your device or shake your device in case you don't have a menu button.
You can simulate pressing such button using `adb` command:
```shell
adb shell input keyevent 82
```

![Developer Menu](https://raw.githubusercontent.com/samfcmc/drafts/master/images/Photos/dev_menu.png)

When the Developer menu appears just press `Enable Live Reload`.
That's it, edit `index.android.js` file and save it. The JS will be reloaded automatically.

One more cool thing...
You can have live reloading even if yo disconnect the USB cable from your computer!
Open Developer Menu and touch `Dev Settings`.

![Dev settings](https://raw.githubusercontent.com/samfcmc/drafts/master/images/Photos/dev_options.png)

Then, touch `Debug server host & port for device`
Make sure your computer and mobile device are connected to the same WiFi network.
Type the IP address of your computer and use 8081 as the port number:
`<Your computer's IP>:8081`

Try to disconnect the USB cable and make some changes to `index.android.js`.
Your app should reload JS automatically.
Running your app on your device without an USB cable...
How cool is that? :)

If you enjoyed this post try to build something using React Native.
I am going to explore a bit more :)
