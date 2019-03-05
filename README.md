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

```
<uses-permission android:name="android.permission.INTERNET" />
```

3. Confirm that you had added the **google-services.json** file to your project’s **app** folder. This step is very important as your project won’t build without this file.

4. Now open the build.gradle located in project’s home directory and add firebase dependency.

```
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.1'
        classpath 'com.google.gms:google-services:4.2.0'
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
```
