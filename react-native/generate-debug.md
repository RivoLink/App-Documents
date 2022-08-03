## Generate a React Native debug on Windows

### Create assets folder
```sh
mkdir android\app\src\main\assets
```

### Generate assets
```sh
npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
```

### Move to android directory
```sh
cd android
```

### Build debug apk
```sh
gradlew assembleDebug
```

### Move to root directory
```sh
cd ..
```

### Open build directory
```sh
start android\app\build\outputs\apk\debug
```
