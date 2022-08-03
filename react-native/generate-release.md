## Build a React Native release apk on Windows

### Generate keystore file
You can change `your_key_name` and `your_key_alias` with any name you want.  
Once you run the keytool utility, you’ll be prompted to type in a password, make sure you remember it.
```sh
keytool -genkey -v -keystore your_key_name.keystore -alias your_key_alias -keyalg RSA -keysize 2048 -validity 10000
```
### Move keystore file to android/app directory
```sh
mv your_key_name.keystore /android/app
```

### Open `android\app\build.gradle` file and add the keystore configuration
```sh
android {
  ....
  signingConfigs {
    release {
      storeFile file('your_key_name.keystore')
      storePassword 'your_keystore_password'
      keyAlias 'your_key_alias'
      keyPassword 'your_keystore_password'
    }
  }
  buildTypes {
    release {
      ....
      signingConfig signingConfigs.release
    }
  }
}
```

### Open `android\app\build.gradle` and update application version
By default: increase `versionCode` by 1 and `versionName` by 0.1
```sh
android {
    ....
    defaultConfig {
        applicationId "your_app_id"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode your_version_code
        versionName "your_version_name"
    }
}
```

### Remove unused files
```sh
rm -rf android/app/src/main/assets
rm -rf android/app/src/main/res/raw
rm -rf android/app/src/main/res/drawable-*
```

### Move to android directory
```sh
cd android
```

### Build release apk
```sh
gradlew clean
gradlew assembleRelease
```

### Move to root directory
```sh
cd ..
```

### Open build directory
```sh
start android\app\build\outputs\apk\release
```

### Reference
[React Native Generate APK — Debug and Release APK](https://medium.com/geekculture/react-native-generate-apk-debug-and-release-apk-4e9981a2ea51)
