# GoogleMapsDemo
Google Maps Demo App for Android using the React Native module, react-native-maps

## Preview
<img src="https://github.com/glowfessorkingslayer/GoogleMapsDemo/blob/master/img/preview1.jpg" width="45%"/> <img src="https://github.com/glowfessorkingslayer/GoogleMapsDemo/blob/master/img/preview2.jpg" width="45%"/>

## My Environment Details
* Computer OS: Windows 10
* Mobile Device OS: Android (only)
* React Native Version: 0.61.5
* react-native-cli: 2.0.1
* Gradle Version: 6.2
* IDE: Visual Studio Code (Build/Run App through Windows Command Line)

## Installation Process

Based off of the [react-native-maps documentation](https://github.com/react-native-community/react-native-maps/blob/master/docs/installation.md)

*Make sure Node.js and yarn are installed on your computer. Also make sure that you add node/npm and yarn to your system's environment PATH variable.*

[Node.js installation](https://nodejs.org/en/download/)

[Yarn installation (AFTER installing Node](https://classic.yarnpkg.com/en/docs/install/#windows-stable)


1. While inside your project directory, install the library from npm:

```sh
npm install react-native-maps --save-exact
```

or from yarn

```sh
yarn add react-native-maps -E
```

2. In order to autolink the react-native-maps module to your project & avoid editing build config files for ANDROID react-native apps, run the following command:
```sh
yarn add react-native-webview
```

3. Install the latest version of [Gradle](https://gradle.org/install/) on your computer. Locate the `gradle-wrapper.properties` folder in `android/gradle/wrapper` and update the Gradle version number in the distributionURL link.

4. Obtain an [API key for the Android Maps SDK](https://developers.google.com/maps/documentation/android-sdk/signup).


## Android Build Configuration for React Native Versions 0.6 and Higher

Please refer to [react-native-maps documentation](https://github.com/react-native-community/react-native-maps) for React Native Versions below 0.6 and for more assistance in the build configuration

> Note: If you choose to clone this repository, the following build configurations are already set.

1. Within your project directory, define *project-wide* properties (__recommended__) in your __ROOT__ `build.gradle`for the react-native-maps library to recognize (depending on:

or do
```
buildscript {
    ext {
        buildToolsVersion = "28.0.3"
        minSdkVersion = 16
        compileSdkVersion = 28
        targetSdkVersion = 28
        supportLibVersion ="28.0.0"
        androidMapsUtilsVersion = "0.6+"
        
        //setting this to the latest version may produce an error, therefore I have kept it at 17.0.0 as of making this project
        playServicesVersion = "17.0.0"
    }
}
...
```

__ONLY__ if you do NOT define *project-wide* properties and/or want to use a different play-services version than the one included in the react-native-maps library, do the following instead (replace '10.0.1' below for desired version):

```groovy
...
dependencies {
   ...
   implementation(project(':react-native-maps')){
       exclude group: 'com.google.android.gms', module: 'play-services-base'
       exclude group: 'com.google.android.gms', module: 'play-services-maps'
   }
   implementation 'com.google.android.gms:play-services-base:10.0.1'
   implementation 'com.google.android.gms:play-services-maps:10.0.1'
}
```

2. Specify your Google Maps API Key:

Add the following code including your API Key to AndroidManifest.xml (`android/app/src/main/AndroidManifest.xml`)

```xml
<application>
   <!-- You will only need to add this meta-data tag, but make sure it's inside the <application> tags -->
   <meta-data
     android:name="com.google.android.geo.API_KEY"
     android:value="Your Google maps API Key Here"/>
</application>
```

> Note: I added my AndroidManifest.xml file to my project's .gitignore file
> in order to avoid committing my Google Maps API Key to my public Github.
> repository. Therefore, if you have cloned this repository, remember to
> create the AndroidManifest.xml file in `android/app/src/main`. Not the most 
> effective way of hiding my API Key from the public, but it is the easiest
> for me for the purposes of committing to my Github repository. Here is 
> my current code inside my AndroidManifest.xml (excluding my API Key):

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
  package="com.googlemapsapidemo">

    <uses-permission android:name="android.permission.INTERNET" />

    <application
      android:name=".MainApplication"
      android:label="@string/app_name"
      android:icon="@mipmap/ic_launcher"
      android:roundIcon="@mipmap/ic_launcher_round"
      android:allowBackup="false"
      android:theme="@style/AppTheme">
      <activity
        android:name=".MainActivity"
        android:label="@string/app_name"
        android:configChanges="keyboard|keyboardHidden|orientation|screenSize"
        android:windowSoftInputMode="adjustResize">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
      </activity>
      <activity android:name="com.facebook.react.devsupport.DevSettingsActivity" />
      <meta-data
        <!-- Keep this line the same, unless stated otherwise by react-naive-maps documentation -->
        android:name="com.google.android.geo.API_KEY"
        android:value="Enter Your Own Google Maps API Key Here"/>
    </application>

</manifest>

```

3. If you are using an Android emulator, make sure it has Google Play Services is installed, [check out this StackOverflow post for more help](https://stackoverflow.com/questions/14536595/how-to-download-google-play-services-in-an-android-emulator).

4. Edit App.js in the root project directory to see the maps

```jsx

import React, { Component } from 'react';
import {
  StyleSheet,
  View,
} from 'react-native';

import MapView, { PROVIDER_GOOGLE } from 'react-native-maps';

export default class App extends Component {
  render() {
    return (
      <View style={styles.container}>
      <MapView
        provider={PROVIDER_GOOGLE} // remove if not using Google Maps
        style={styles.map}
        region={{
        //you can change latitude & longitude to set your desired location
        latitude: 32.9857619,
        longitude: -96.7500993,
        latitudeDelta: 0.015,
        longitudeDelta: 0.0121,
        }}
      />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  map: {
    flex: 1
  }
});
```

> Note: If you are using Android Studio or want iOS compatibility, refer to
> the [react-native-maps documentation](https://github.com/react-native-community/react-native-maps)
