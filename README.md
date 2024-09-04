## Prerequisite
- NVM
- Node v12.22.12 LTS
## How to
`npx @react-native-community/cli@latest init AwesomeProject --version 0.63.2`

### Tested in Macbook Pro 13inch 2015 (Intel) MacOS Monterey
#### iOS
- Xcode 14.0
- Cocoapods 1.15.2
- Comment Flipper for fix Error
```
#  use_flipper!
#  post_install do |installer|
#    flipper_post_install(installer)
#  end
```
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
