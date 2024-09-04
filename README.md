## Prerequisite
- NVM
- Node v12.22.12 LTS
## How to
`npx @react-native-community/cli@latest init AwesomeProject --version 0.63.2`

### Tested in Macbook Pro 13inch 2015 (Intel) MacOS Monterey
<img width="1680" alt="Screen Shot 2024-09-04 at 12 32 58" src="https://github.com/user-attachments/assets/b144661c-7bdd-4468-aede-273fc4ffa593">

#### iOS ✅
- Xcode 14.0
- Cocoapods 1.15.2
- Comment Flipper for fix Error
```
#  use_flipper!
#  post_install do |installer|
#    flipper_post_install(installer)
#  end
```
<img width="1680" alt="Screen Shot 2024-09-04 at 10 53 43" src="https://github.com/user-attachments/assets/a3c93d74-6bd4-40ce-b2bd-390443ac8fc4">

#### Android ✅
- Android Studio Koala | 2024.1.1 Patch 2
- Comment this code at `build.gradle | Module`
```
//    debugImplementation("com.facebook.flipper:flipper:${FLIPPER_VERSION}") {
//      exclude group:'com.facebook.fbjni'
//    }
//
//    debugImplementation("com.facebook.flipper:flipper-network-plugin:${FLIPPER_VERSION}") {
//        exclude group:'com.facebook.flipper'
//        exclude group:'com.squareup.okhttp3', module:'okhttp'
//    }
//
//    debugImplementation("com.facebook.flipper:flipper-fresco-plugin:${FLIPPER_VERSION}") {
//        exclude group:'com.facebook.flipper'
//    }
```
```
// Run this once to be able to run the application with BUCK
// puts all compile dependencies into folder libs for BUCK to use
//task copyDownloadableDepsToLibs(type: Copy) {
//    from configurations.compile
//    into 'libs'
//}
```
- Change `distributionUrl` gradle to 7.3 for Android Studio Koala
```
distributionUrl=https\://services.gradle.org/distributions/gradle-7.3-all.zip
```
- Change `com.android.tools.build:gradle` version to 7.0.0
```
dependencies {
    classpath("com.android.tools.build:gradle:7.0.0")
    // NOTE: Do not place your application dependencies here; they belong
    // in the individual module build.gradle files
}
```
- Remove `ReactNativeFlipper.java`
- Remove or comment this code at `MainApplication.java`
```
initializeFlipper(this, getReactNativeHost().getReactInstanceManager());
```
```
 /**
   * Loads Flipper in React Native templates. Call this in the onCreate method with something like
   * initializeFlipper(this, getReactNativeHost().getReactInstanceManager());
   *
   * @param context
   * @param reactInstanceManager
   */
  private static void initializeFlipper(
      Context context, ReactInstanceManager reactInstanceManager) {
    if (BuildConfig.DEBUG) {
      try {
        /*
         We use reflection here to pick up the class that initializes Flipper,
        since Flipper library is not available in release mode
        */
        Class<?> aClass = Class.forName("com.awesomeproject.ReactNativeFlipper");
        aClass
            .getMethod("initializeFlipper", Context.class, ReactInstanceManager.class)
            .invoke(null, context, reactInstanceManager);
      } catch (ClassNotFoundException e) {
        e.printStackTrace();
      } catch (NoSuchMethodException e) {
        e.printStackTrace();
      } catch (IllegalAccessException e) {
        e.printStackTrace();
      } catch (InvocationTargetException e) {
        e.printStackTrace();
      }
    }
  }
```
<img width="1680" alt="Screen Shot 2024-09-04 at 11 30 39" src="https://github.com/user-attachments/assets/5f48b491-7b13-46ca-8954-135992d736f3">


### Tested in Macbook Pro 16inch 2021 (Apple Silicon) MacOS Sonoma
<img width="1136" alt="Screenshot 2024-09-04 at 12 34 53" src="https://github.com/user-attachments/assets/12343c0d-c0c7-48fa-9551-4406265052ab">

#### iOS ❌
- Xcode 15.2
<img width="1136" alt="Screenshot 2024-09-04 at 10 36 25" src="https://github.com/user-attachments/assets/8d45ca97-687b-480f-9c03-5c6d10895e0e">
<img width="1512" alt="Screenshot 2024-09-04 at 10 39 30" src="https://github.com/user-attachments/assets/66066c7a-743e-4f3f-95f1-fbc11eccce41">

#### Android ❌ -> ✅
- Android Studio Koala | 2024.1.1 Patch 2
- Error when run from Android without Metro started first
<img width="2056" alt="Screenshot 2024-09-04 at 12 28 21" src="https://github.com/user-attachments/assets/25cc53c6-7d77-497f-a458-c16ab99938b1">
- Error when use `npm run android`
<img width="2056" alt="Screenshot 2024-09-04 at 12 29 28" src="https://github.com/user-attachments/assets/068c83bb-f72b-4660-9469-8775a9626e91">

- Its working when we start metro first and run by Android Strudio
`npm start` then run on `Android Studio`
<img width="2056" alt="Screenshot 2024-09-04 at 12 23 53" src="https://github.com/user-attachments/assets/b784f513-76af-4cf0-8137-cf352d2a5a1c">

