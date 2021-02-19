# React Native Command

## Clear cache

- Clear cache android

```sh
cd android && ./gradlew clean && cd ..
```

- Clear cache npm 

```sh
npm cache clean --force
```

## Run app

- Run node service

  + Use npm: 
  ```sh
  npm run start
  ```

   + Use yarn: 
  ```sh
  yarn start
  ```

  + Run with reset cache: 
  ```sh
  yarn start --reset-cache
  ```

- Run app android

```sh
react-native run-android
```

- Run app ios

```sh
react-native run-ios
```

- Run app ios with simulator

```sh
react-native run-ios --simulator="iPhone 11 Pro Max"
```

  + To show list simulator run command

  ```sh
  xcrun simctl list devices
  ```

## Logs

- Show log native android

```sh
adb logcat
```

- Show log native android

```sh
adb logcat --pid=`adb shell pidof -s com.yourpackage`
```

## Build app

- Build app android release

```sh
cd android && ./gradlew assembleRelease && cd .. 
```

- Build app android bundle release

```sh
cd android && ./gradlew bundleRelease && cd .. 
```

- Build app android release debug

  + Step 1 run command

  ```sh
  react-native bundle --dev false --platform android --entry-file index.js --bundle-output ./android/app/src/main/assets/index.android.bundle --assets-dest ./android/app/src/main/res
  ```

  + Step 2 run

  ```sh
  cd android && ./gradlew assembleDebug && cd ..
  ```

## Simulator

- Open emulator android

  + Show list emulator android

  ```sh
  emulator -list-avds
  ```

  + Open emulator

  ```sh
  /Users/YourComputerName/Library/Android/sdk/emulator/emulator -avd EmulatorName -netdelay none -netspeed full
  ```

  > YourComputerName: Your computer name (Ex: MyComputer)
  
  > EmulatorName: Emulator name (Ex: Pixel_3a_API_30_x86)


# NPM

## Login

- Login normal

```sh
npm login
```

- Login with scope

```sh
npm login —scope=@[scope]
```

## Profile

- Create profile

```sh
npm init —scope=@[scope]
```

- Switch scope

```sh
npmrc [profile-name]
```

## Publish

- Publish

```sh
npm publish --access public
```

- Unpublish

```sh
npm unpublish -f @[scope]/[package-name]n@[version]
```

> (-f --> force)

# Github

## Tag

- Create Tag

```sh
git tag v1.0.0
```

- Pushing a Tag

```sh
git push origin v1.0.0
```

# Keystore & keychain

- Create keystore

```sh
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

- Create SHA-1 certificate fingerprints

```sh
keytool -list -v -keystore PathToYourApp/android/app/my-release-key.keystore -alias my-key-alias -storepass mystorepass -keypass mykeypass
```

- Copy ssh key

```sh
pbcopy < ~/.ssh/id_rsa.pub
```

# Deeplink

## Open app android

```sh
adb shell am start -a android.intent.action.VIEW -d "your-deep-link” app-package-name
```

# Some error with react native

1. Error verifyReleaseResources

```java
// add to bottom of file android/build.gradle
subprojects {
    afterEvaluate {project ->
        if (project.hasProperty("android")) {
            android {
                compileSdkVersion rootProject.ext.compileSdkVersion
                buildToolsVersion rootProject.ext.buildToolsVersion
            }
        }
    }
}
```

2. Error can't call api with http on android

```java
// add to application tag of AndroidManifest.xml file
android:usesCleartextTraffic="true"
```