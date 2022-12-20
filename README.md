# Pitel
## How to fix the crash error "Didn’t find class on path DexPathList"

File `android/build.gradle`:

```diff
buildscript {
    ...
    dependencies {
-       classpath("com.android.tools.build:gradle:4.1.3")
+       classpath("com.android.tools.build:gradle:4.2.2")
    }
}
```
File `android/app/build.gradle`:
```diff
android {
    ...
    defaultConfig {
    ...
+       multiDexEnabled true
    }
    ...
    buildTypes {
        debug {
            ...
+           minifyEnabled true
+           shrinkResources  true
+           proguardFiles getDefaultProguardFile("proguard-android.txt"), "proguard-rules.pro"
        }
    }
}
```
File `android/app/proguard-rules.pro`
```diff
# define which package or class not found on path DexPathList 
--keep class org.webrtc.** { *; }
+-keep class org.webrtc.** { *; }
+-keep class <your package>.** { *; }
```
## References
https://developer.android.com/studio/build/shrink-code

https://developer.android.com/studio/build/multidex
