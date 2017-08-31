# android-react-native-integration-example

Example android project that embedded with react native view. Basically [the official guide](https://facebook.github.io/react-native/docs/integration-with-existing-apps.html) is not working. Use the project to indentify what's wrong and missing in the guide. 

---
```
npm install --save react react-native
```
is not working because react-native depends on alpha version of react, but npm install react will install stable version instead.
```
npm install --save react@16.0.0-alpha.12 react-native@0.47.2
```

--- 
```
allprojects {
    repositories {
        ...
        maven {
            // All of React Native (JS, Android binaries) is installed from npm
            url "$rootDir/node_modules/react-native/android"
        }
    }
    ...
}
```
should be 
```
allprojects {
    repositories {
        ...
        maven {
            // All of React Native (JS, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
    }
    ...
}
```

---
`build.gradle` need to have
```
compile 'com.android.support:appcompat-v7:23.0.1'
```

---
```
AppRegistry.registerComponent('AwesomeProject', () => HelloWorld);
```
needs to be following to match `mReactRootView.startReactApplication(mReactInstanceManager, "HelloWorld", null);
`
```
AppRegistry.registerComponent('HellWorld', () => HelloWorld);
```
---
```
mReactInstanceManager.onHostDestroy();
```
needs to be following to avoid deprecated method
```
mReactInstanceManager.onHostDestroy(this);
```