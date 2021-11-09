# graphQL cheat sheet

+ NOTE this cheatsheet comes after you done with amplify cheatsheet.

___

## Configure API

### To start provisioning API resources in the backend, go to your project directory and execute this command:

```
amplify add api
```

### Enter the following when prompted:

```
? Please select from one of the below mentioned services: 
    `GraphQL`
? Provide API name: 
    `apiName`
? Choose the default authorization type for the API:
    `API key`
? Enter a description for the API key:
    `description`
? After how many days from now the API key should expire (1-365): 
    `7`
? Do you want to configure advanced settings for the GraphQL API 
    `No, I am done.`
? Do you have an annotated GraphQL schema? 
    `No`
? Choose a schema template:
    `Single object with fields (e.g., “Todo” with ID, name, description)`
? Do you want to edit the schema now? 
    `No`
```

___

### now open your android project, The guided schema creation will output amplify/backend/api/{api_name}/schema.graphql containing the following:

```
type Todo @model {
  id: ID!
  name: String!
  description: String
}
```

### modify the schema as you need then run this command To push your changes to the cloud:

```
amplify push
```

### Enter the following when prompted:

```
? Do you want to generate code for your newly created GraphQL API 
    `No`
```

___

### now we need to generate the model class based on the schema we pushed before by running this command:

```
amplify codegen models
```


### after that open build.gradle (Module) and add these dependencies then run gradle sync:

```
dependencies {
    implementation 'com.amplifyframework:core:1.24.0'
    implementation 'com.amplifyframework:aws-api:1.24.0'
}
```

___

### now we want to initialize the Amplify API category by adding this code to our onCreate function which is inside the MainActivity of the app, just make it look like this by adding the first line of code to the code we added before in the installation of amplify:

```
 try {
            // Add this line to add the AWSApiPlugin plugins
            Amplify.addPlugin(new AWSApiPlugin());
            Amplify.configure(getApplicationContext());
            Log.i("MyAmplifyApp", "Initialized Amplify");
        } catch (AmplifyException error) {
            Log.e("MyAmplifyApp", "Could not initialize Amplify", error);
        }
```

___

### now the graphQL is ready and you can create an object and save it to the graphQL database by using this code (modify it as you need):

```
Todo todo = Todo.builder()
    .name("My first todo")
    .description("todo description")
    .build();
Amplify.API.mutate(
    ModelMutation.create(todo),
    response -> Log.i("MyAmplifyApp", "Added Todo with id: " + response.getData().getId()),
    error -> Log.e("MyAmplifyApp", "Create failed", error)
);
```
