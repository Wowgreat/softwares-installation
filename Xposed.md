#### Install Xposed

Write later



#### How Xposed Works



#### Creating the project

##### Adding the Xposed Framework API to your project

###### Gradle

``` 
# app/build.grade
dependencies {
    provided 'de.robv.android.xposed:api:82' # add it
}
```

**It is very important that you use provided instead of compile!**  The latter would include the API classes in your APK, Which can cause issues especially on Android 4.x. Using `provided` just makes the API classes usable from your modulem but there will only be referebces to them in the APK. The actual implementation will be `provided` when user installs the Xposed Framework.

In most cases, the `repositories` block already exists, and there are usually some dependencies already. In that case, you just need to add the `provided` line to the existing `dependencies` block.

Unfortunately, I didn't find any good way to enable automatic download of the API sources, except using *both* of these lines:

```
provided 'de.robv.android.xposed:api:82'
provided 'de.robv.android.xposed:api:82:sources'
```

 Please make sure to **disable Instant Run** (`File -> Settings -> Build, Execution, Deployment -> Instant Run`), otherwise your classes aren't included directly in the APK, but loaded via a stub application which Xposed can't handle.

###### assets/xposed_init

The only thing that is still missing now is a hint for XposedBridge which classes contain such entry points. This is done via a file called `xposed_init`. Create a new text file with that name in the `assets` folder. In this file, each line contains one fully qualified class name. In this case, this is `{package}.{class}`

