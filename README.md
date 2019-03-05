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

6. Add the below resources to **dimens.xml, colors.xml and strings.xml**. These resources doesn’t require for firebase, but for this demo.

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

#### `strings.xml`

```xml
<resources>
    <string name="app_name">Firebase Auth</string>
    <string name="action_sign_in_short">Register</string>
    <string name="email">Email</string>
    <string name="minimum_password">Password too short, enter minimum 6 characters!</string>
    <string name="auth_failed">Authentication failed, check your email and password or sign up</string>
    <string name="change_email">Change Email</string>
    <string name="change_password">Change Password</string>
    <string name="send_password_reset_email">Send Password reset email</string>
    <string name="remove_user">Remove user</string>
    <string name="new_pass">New Password</string>
    <string name="title_activity_profile">Firebase</string>
    <string name="title_activity_login">Sign in</string>
    <string name="hint_email">Email</string>
    <string name="hint_password">Password</string>
    <string name="hint_name">Fullname</string>
    <string name="btn_login">LOGIN</string>
    <string name="btn_link_to_register">Not a member? Get registered in Firebase now!</string>
    <string name="btn_link_to_login">Already registered. Login Me!</string>
    <string name="title_activity_reset_password">ResetPasswordActivity</string>
    <string name="btn_forgot_password">Forgot your password?</string>
    <string name="btn_reset_password">Reset Password</string>
    <string name="btn_back"><![CDATA[<< Back]]></string>
    <string name="hint_new_email">New Email</string>
    <string name="btn_change">Change</string>
    <string name="btn_send">Send</string>
    <string name="btn_remove">Remove</string>
    <string name="btn_sign_out">Sign Out</string>
    <string name="lbl_forgot_password">Forgot password?</string>
    <string name="forgot_password_msg">We just need your registered Email Id to sent you password reset instructions.</string>
</resources>
```

#### **Now we have the project ready with all the dependencies added. Let’s start by adding the sign up screen.**

## SIGNUP WITH EMAIL & PASSWORD.

7. Create an activity named **SignupActivity.java** and add the following code to the layout file **activity_signup.xml**

#### `activity_signup.xml`

```xml

<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:context=".SignupActivity">
 
    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:background="@color/colorPrimaryDark"
        android:gravity="center"
        android:orientation="vertical"
        android:padding="@dimen/activity_horizontal_margin">
 
 
        <ImageView
            android:layout_width="@dimen/logo_w_h"
            android:layout_height="@dimen/logo_w_h"
            android:layout_gravity="center_horizontal"
            android:layout_marginBottom="30dp"
            android:src="@mipmap/ic_launcher" />
 
        <android.support.design.widget.TextInputLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
 
            <EditText
                android:id="@+id/email"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="@string/email"
                android:inputType="textEmailAddress"
                android:maxLines="1"
                android:singleLine="true"
                android:textColor="@android:color/white" />
 
        </android.support.design.widget.TextInputLayout>
 
        <android.support.design.widget.TextInputLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
 
            <EditText
                android:id="@+id/password"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:focusableInTouchMode="true"
                android:hint="@string/hint_password"
                android:imeActionId="@+id/login"
                android:imeOptions="actionUnspecified"
                android:inputType="textPassword"
                android:maxLines="1"
                android:singleLine="true"
                android:textColor="@android:color/white" />
 
        </android.support.design.widget.TextInputLayout>
 
        <Button
            android:id="@+id/sign_up_button"
            style="?android:textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="16dp"
            android:background="@color/colorAccent"
            android:text="@string/action_sign_in_short"
            android:textColor="@android:color/black"
            android:textStyle="bold" />
 
        <Button
            android:id="@+id/btn_reset_password"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="20dip"
            android:background="@null"
            android:text="@string/btn_forgot_password"
            android:textAllCaps="false"
            android:textColor="@color/colorAccent" />
 
        <!-- Link to Login Screen -->
 
        <Button
            android:id="@+id/sign_in_button"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="20dip"
            android:background="@null"
            android:text="@string/btn_link_to_login"
            android:textAllCaps="false"
            android:textColor="@color/white"
            android:textSize="15dp" />
    </LinearLayout>
 
    <ProgressBar
        android:id="@+id/progressBar"
        android:layout_width="30dp"
        android:layout_height="30dp"
        android:layout_gravity="center|bottom"
        android:layout_marginBottom="20dp"
        android:visibility="gone" />
</android.support.design.widget.CoordinatorLayout>
```

8. Open **SignupActivity.java** and add the following. Firebase provides **createUserWithEmailAndPassword()** method to create a new user with email and password data.


#### `SignupActivity.java`

```java

package com.zecolloauth.zecolloauth;

import android.content.Intent;
import android.os.Bundle;
import android.support.annotation.NonNull;
import android.support.v7.app.AppCompatActivity;
import android.text.TextUtils;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ProgressBar;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class SignupActivity extends AppCompatActivity {

    private EditText inputEmail, inputPassword;
    private Button btnSignIn, btnSignUp, btnResetPassword;
    private ProgressBar progressBar;
    private FirebaseAuth auth;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_signup);

        //Get Firebase auth instance
        auth = FirebaseAuth.getInstance();

        btnSignIn = (Button) findViewById(R.id.sign_in_button);
        btnSignUp = (Button) findViewById(R.id.sign_up_button);
        inputEmail = (EditText) findViewById(R.id.email);
        inputPassword = (EditText) findViewById(R.id.password);
        progressBar = (ProgressBar) findViewById(R.id.progressBar);
        btnResetPassword = (Button) findViewById(R.id.btn_reset_password);

        btnResetPassword.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(new Intent(SignupActivity.this, ResetPasswordActivity.class));
            }
        });

        btnSignIn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish();
            }
        });

        btnSignUp.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                String email = inputEmail.getText().toString().trim();
                String password = inputPassword.getText().toString().trim();

                if (TextUtils.isEmpty(email)) {
                    Toast.makeText(getApplicationContext(), "Enter email address!", Toast.LENGTH_SHORT).show();
                    return;
                }

                if (TextUtils.isEmpty(password)) {
                    Toast.makeText(getApplicationContext(), "Enter password!", Toast.LENGTH_SHORT).show();
                    return;
                }

                if (password.length() < 6) {
                    Toast.makeText(getApplicationContext(), "Password too short, enter minimum 6 characters!", Toast.LENGTH_SHORT).show();
                    return;
                }

                progressBar.setVisibility(View.VISIBLE);
                //create user
                auth.createUserWithEmailAndPassword(email, password)
                        .addOnCompleteListener(SignupActivity.this, new OnCompleteListener<AuthResult>() {
                            @Override
                            public void onComplete(@NonNull Task<AuthResult> task) {
                                Toast.makeText(SignupActivity.this, "createUserWithEmail:onComplete:" + task.isSuccessful(), Toast.LENGTH_SHORT).show();
                                progressBar.setVisibility(View.GONE);
                                // If sign in fails, display a message to the user. If sign in succeeds
                                // the auth state listener will be notified and logic to handle the
                                // signed in user can be handled in the listener.
                                if (!task.isSuccessful()) {
                                    Toast.makeText(SignupActivity.this, "Authentication failed." + task.getException(),
                                            Toast.LENGTH_SHORT).show();
                                } else {
                                    startActivity(new Intent(SignupActivity.this, MainActivity.class));
                                    finish();
                                }
                            }
                        });

            }
        });
    }

    @Override
    protected void onResume() {
        super.onResume();
        progressBar.setVisibility(View.GONE);
    }
}
```

9. Open AndroidManifest.xml and make SignupActivity as **launcher activity (temporarily)** and test the sign up.

























































Developed by
========================



Check  on color xml
stringxml
dimex xml
app theme color
layout 
activities