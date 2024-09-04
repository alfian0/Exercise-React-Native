## Prerequisite
- NVM
- Node v12.22.12 LTS
## How to
`npx @react-native-community/cli@latest init AwesomeProject --version 0.63.2`

### Tested in Macbook Pro 13inch 2015 (Intel) MacOS Monterey
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

#### Android
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
### Tested in Macbook Pro 16inch 2021 (Apple Silicon) MacOS Sonoma
#### iOS ❌
<img width="1136" alt="Screenshot 2024-09-04 at 10 36 25" src="https://github.com/user-attachments/assets/8d45ca97-687b-480f-9c03-5c6d10895e0e">
<img width="1512" alt="Screenshot 2024-09-04 at 10 39 30" src="https://github.com/user-attachments/assets/66066c7a-743e-4f3f-95f1-fbc11eccce41">

#### Android ❌
![Screenshot_20240904_104524](https://github.com/user-attachments/assets/497bc4d5-be8c-4d3d-a3f1-f3a82b9c80ee)
