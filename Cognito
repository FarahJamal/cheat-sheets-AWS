# Cognito cheat sheet

## Configure Auth Category

### To start provisioning auth resources in the backend, go to your project directory and execute the command:

```
amplify add auth
```

### Enter the following when prompted:

```
? Do you want to use the default authentication and security configuration?
    `Default configuration`
? How do you want users to be able to sign in?
    `Username`
? Do you want to configure advanced settings?
    `No, I am done.`
```

### now excute this command To push your changes to the cloud:

```
amplify push
```

___

### now open your android project, and add this to the dependencies inside the gradle(module):

```
dependencies {
    implementation 'com.amplifyframework:aws-auth-cognito:1.24.0'
}
```

___

### Add the Auth plugin before calling Amplify.configure in the onChange function inside the MainActivity:

```
// Add this line, to include the Auth plugin.
Amplify.addPlugin(new AWSCognitoAuthPlugin());
```

___

## Register a user:

### to register a user use this code (modify the email, username , password  as what the user input in the form):

```
AuthSignUpOptions options = AuthSignUpOptions.builder()
    .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
    .build();
Amplify.Auth.signUp("username", "Password123", options,
    result -> Log.i("AuthQuickStart", "Result: " + result.toString()),
    error -> Log.e("AuthQuickStart", "Sign up failed", error)
);
```

### A confirmation code will be sent to the email id provided during sign up , use this code in the confirmation page (change username as the username of the user who just registered, and change the code you received via email as the code user should input on the confirmation page).

```
Amplify.Auth.confirmSignUp(
    "username",
    "the code you received via email",
    result -> Log.i("AuthQuickstart", result.isSignUpComplete() ? "Confirm signUp succeeded" : "Confirm sign up not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

___


## Sign in

### Implement a UI to get the username and password from the user. After the user enters the username and password you can start the sign in flow by calling the following method:

```
Amplify.Auth.signIn(
    "username",
    "password",
    result -> Log.i("AuthQuickstart", result.isSignInComplete() ? "Sign in succeeded" : "Sign in not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

___

## Sign out

### Invoke the signOut api to sign out a user from the Auth category.

```
Amplify.Auth.signOut(
    () -> Log.i("AuthQuickstart", "Signed out successfully"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

### second way to sign out from all devices:

```
Amplify.Auth.signOut(
    AuthSignOutOptions.builder().globalSignOut(true).build(),
    () -> Log.i("AuthQuickstart", "Signed out globally"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```
