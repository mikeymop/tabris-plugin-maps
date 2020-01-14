# Tabris Plugin Maps

You will want to open the `project/android` folder in Android Studio.

When you first open the project in Android Studio you will have to resolve the dependencies before you begin building the application.
You can do this by modifying the following two files:

* ./build.gradle (project: gradle)
* maps/build.gradle (module: gradle)

If you look in `src/android/../maps` you will see several kotlin files for example `CameraProperty.kt`.

It imports the following:

```kotlin
import com.eclipsesource.tabris.android.V8ObjectProperty
import com.eclipsesource.tabris.android.internal.ktx.toList
import com.eclipsesource.v8.V8Object
import com.google.android.gms.maps.CameraUpdateFactory
import com.google.android.gms.maps.model.LatLng
```

We will need to import these packages into our local maven repo using gradle tasks. Android Studio can handle this for us.

Go to `File > Project Structure > Dependencies`, click `+` and search for `com.eclipsesource`

Click and add the latest version of all of the needed modules and hit apply.

### Using the proper j2v8 lib for your platform

J2V8 converts Java to Node v8 javascript classes, because this depends on java bytecode it is platform specific.
You will want to look on [Maven Central](https://search.maven.org/search?q=com.eclipsesource.j2v8) and look for the latest version that has the correct artifact id for your platform.

In the case of a 64bit Linux operating system we would want to use `j2v8_linux_x86_64` or compile the library ourselves.

In our `module/build.gradle` we will specify the option on it's depdency declaration:

```
dependencies {
  implementation 'com.eclipsesource.tabris.android:tabris:3.2.1'
  implementation 'com.google.android.gms:play-services-maps:17.0.0'
  implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
  implementation 'com.eclipsesource.j2v8:j2v8_linux_x86_64:4.8.0' // notice the platform version
}
```

Notice that I have included the platform and it's latest version in the last dependency declaration.
