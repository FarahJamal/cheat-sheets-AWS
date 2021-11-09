# amplify cheat sheet

## Installation

Open your terminal, and run this command to install amplify CLI globally.

### to install it with NPM (recommended):

+ NOTE because we are installing it globally you might need to run the command with sudo

```
npm install -g @aws-amplify/cli
```

### to install it with cURL (windows):

```
curl -sL https://aws-amplify.github.io/amplify-cli/install-win -o install.cmd && install.cmd
```

### to install it with cURL (linux or mac):

```
curl -sL https://aws-amplify.github.io/amplify-cli/install | bash && $SHELL
```

___

### Now it's time to setup the Amplify CLI. Configure Amplify by running the following command:

```
amplify configure
```

### after running the amplify configure command, answer everything as below

```
Specify the AWS Region
? region:  # Your preferred region
Specify the username of the new IAM user:
? user name:  # User name for Amplify IAM user
Complete the user creation using the AWS console
```

1. after the above, amplify will ask you to sign into the AWS Console (from browser).
2. Once you're signed in, create an IAM user with an AdministratorAccess (from browser).

### when you done with creating the IAM user , the terminal will ask you these questions answer them as below

```
Enter the access key of the newly created user:
? accessKeyId:  # YOUR_ACCESS_KEY_ID
? secretAccessKey:  # YOUR_SECRET_ACCESS_KEY
This would update/create the AWS Profile in your local machine
? Profile Name:  # (default)
Successfully set up the new user.
```

___

### now open your project and inside the build.gradle (Module) add the following lines, then run gradle sync

```
android {
    compileOptions {
        // Support for Java 8 features
        coreLibraryDesugaringEnabled true
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
dependencies {
    // Amplify core dependency
    implementation 'com.amplifyframework:core:1.24.0'
    // Support for Java 8 features
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:1.1.5'
}
```

### now in your project and inside the build.gradle (Project) add the following lines, then run gradle sync

```
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:4.1.2'
        // Add this line into `dependencies` in `buildscript`
        classpath 'com.amplifyframework:amplify-tools-gradle-plugin:1.0.2'
    }
}
allprojects {
    repositories {
        google()
        jcenter()
    }
}
// Add this line at the end of the file
apply plugin: 'com.amplifyframework.amplifytools'
```

___


### To start provisioning resources in the backend, you must be in your project directory then run this command

```
amplify init
```

### Enter the following when prompted:

```
? Enter a name for the project
    `MyAmplifyApp`
? Initialize the project with the above configuration?
    `No`
? Enter a name for the environment
    `dev`
? Choose your default editor:
    `Android Studio`
? Choose the type of app that you're building
    `android`
? Where is your Res directory:
    `app/src/main/res`
? Select the authentication method you want to use:
    `AWS profile`
? Please choose the profile you want to use
    `default`
```

___

### after that, inside your MainActivity class in your project add this code at the beginning of onCreate function

```
try {
          Amplify.configure(getApplicationContext());
          Log.i("MyAmplifyApp", "Initialized Amplify");
      } catch (AmplifyException error) {
          Log.e("MyAmplifyApp", "Could not initialize Amplify", error);
      }
  }
```

### now run the build and you should see this in the logcat , put this inside its search =>(MyAmplifyApp)

```
com.example.MyAmplifyApp I/MyAmplifyApp: Initialized Amplify
```
