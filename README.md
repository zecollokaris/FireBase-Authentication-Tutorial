# <p align="center">FIREBASE AUTHENTICATION<p>

## ENABLING FIREBASE AUTH

1. First thing you need to do is go to `https://firebase.google.com/` and make an account to gain access to their console. After you gain access to the console you can start by creating your first project.

######IMAGE OF CREATED PROJECT!########

- **Give your project a name of your choice.**

######IMAGE OF CREATING PROJECT!########

2. Next go to your project dashboard. Find the Auth and click get started. Go to set up sign in method and choose Email & Password and enable it.

######CROPED IMAGE OF ADDING EMAIL OUTH!########

3. We need to now add Firebase to our android app so go to the project overview section and choose android.

######IMAGE OF CHOOSING ANDROID!########

3. Give the package name of your project (mine is com.zecolloauth.zecolloauth) in which you are going to integrate the Firebase. 

######IMAGE OF ADDING PACKAGE NAME!########

4. Here the google-services.json file will be downloaded when you press add app button.

######IMAGE OF DOWNLOADING GOOGLE FILE!########

5. Switch to the Project view in Android Studio to see your project root directory. Move the **google-services.json** file you just downloaded into your Android app module `app/src/main` root directory.

######IMAGE OF ADDING THE JSON FILE!########

## CREATING ANDROID PROJECT

**As we work here you can compare some section of your code with my repository incase you get stuck!**

1. Create a new project in Android Studio from **File ⇒ New Project.** When it prompts you to select the default activity, select **Blank Activity** and proceed.

While filling the project details, use the same package name which you gave in firebase console. In my case I am using same **com.zecolloauth.zecolloauth**.

2. Open **AndroidManifest.xml** and add the **INTERNET** permission as we need to **make network calls.**

#### `AndroidManifest.xml`

```
<uses-permission android:name="android.permission.INTERNET" />
```

3. Confirm that you had added the **google-services.json** file to your project’s **app** folder. This step is very important as your project won’t build without this file.

4. Now open the **build.gradle** located in project’s home directory and add firebase dependency.

#### `build.gradle`

```
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.1'
        classpath 'com.google.gms:google-services:4.2.0'
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
```

5. Open **app/build.gradle** and add firebase auth dependency. At the very bottom of the file, add **apply plugin: ‘com.google.gms.google-services’**

#### `app/build.gradle`

```
dependencies {
    implementation 'com.google.firebase:firebase-auth:9.0.2'
}
 
apply plugin: 'com.google.gms.google-services'
```

6. Add the below resources to dimens.xml, colors.xml and strings.xml. These resources doesn’t require for firebase, but for this article.

#### `dimex.xml`

```xml
<resources>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>
    <dimen name="fab_margin">16dp</dimen>
    <dimen name="logo_w_h">100dp</dimen>
</resources>
```

#### `colors.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#00bcd4</color>
    <color name="colorPrimaryDark">#0097a7</color>
    <color name="colorAccent">#f2fe71</color>
 
    <color name="bg_login">#26ae90</color>
    <color name="bg_register">#2e3237</color>
    <color name="bg_main">#428bca</color>
    <color name="white">#ffffff</color>
    <color name="input_login">#222222</color>
    <color name="input_login_hint">#999999</color>
    <color name="input_register">#888888</color>
    <color name="input_register_bg">#3b4148</color>
    <color name="input_register_hint">#5e6266</color>
    <color name="btn_login">#26ae90</color>
    <color name="btn_login_bg">#eceef1</color>
    <color name="lbl_name">#333333</color>
    <color name="btn_logut_bg">#ff6861</color>
</resources>
```









































Developed by
========================