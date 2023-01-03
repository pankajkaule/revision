<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. what is Amplify? ?</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => The open-source Amplify provides the following products to build fullstack iOS, Android, Flutter, Web, and React Native apps:

1. Amplify CLI - Configure all the services needed to power your backend through a simple command line interface.
2. Amplify Libraries - Use case-centric client libraries to integrate your app code with a backend using declarative interfaces.
3. Amplify UI Components - UI libraries for React, React Native, Angular, Vue and Flutter.\

The Amplify Hosting is an AWS service that provides a git-based workflow for continuous deployment & hosting of fullstack web apps. Cloud resources created by the Amplify CLI are also visible in the Amplify Console. .</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. How to Install and configure the Amplify CLI ?</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => 

[video link](https://youtu.be/fWbM5DLh25U)

steps

1. npm install -g @aws-amplify/cli

Now it's time to setup the Amplify CLI. Configure Amplify by running the following command:


2. amplify configure

Once you're signed in, Amplify CLI will ask you to create an IAM user.

Specify the AWS Region
? region:  <Your preferred region>
Specify the username of the new IAM user:
? user name:  <User name for Amplify IAM user>
Complete the user creation using the AWS console: <URL>

Follow the <URL> and create a user with AdministratorAccess-Amplify to your account to provision AWS resources for you like AppSync, Cognito etc.

<img src='./assets/user-creation.gif'>

Amplify CLI will then ask you to copy and paste the accessKeyId and the secretAccessKey from your newly created IAM user to connect with Amplify CLI.

Enter the access key of the newly created user:
? accessKeyId:  <ACCESSKEYID>
? secretAccessKey:  <ACCESSKEY>
This would update/create the AWS Profile in your local machine
? Profile Name: default
Successfully set up the new user.

In the next section, you'll set up the app and initialize Amplify.


3. Create a new React App

To get started, first create a new React app, and then install and use the Amplify CLI to start adding backend capabilities to your app.

From your projects directory, run the following commands:

```cli

npx create-react-app react-amplified
cd react-amplified

```

This creates a new React app in a directory called react-amplified and then switches into the new directory.

From the react-amplified directory, run the app by using the following command:

```console
npm start
```

4. Initialize a new backend

With the app running, it's time to set up Amplify and create the backend services to support the app.

Open a new terminal. From the react-amplified directory, run:


```console

amplify init
```

When you initialize Amplify you'll be prompted for some information about the app, with the option to accept recommended values:


```python
? Enter a name for the project reactamplified
The following configuration will be applied:

?Project information
| Name:  reactamplified
| Environment: dev
| Default editor: Visual Studio Code
| App type: javascript
| Javascript framework: react
| Source Directory Path: src
| Distribution Directory Path: build
| Build Command: npm run-script build
| Start Command: npm run-script start
? Initialize the project with the above configuration? Yes
Using default provider  awscloudformation
? Select the authentication method you want to use: AWS profile

...

? Please choose the profile you want to use default
```
When you initialize a new Amplify project, a few things happen:

1. It creates a top level directory called amplify that stores your backend definition. During the tutorial you'll add capabilities such as a GraphQL API and authentication. As you add features, the amplify folder will grow with infrastructure-as-code templates that define your backend stack. 
2. Infrastructure-as-code is a best practice way to create a replicable backend stack.
It creates a file called aws-exports.js in the src directory that holds all the configuration for the services you create with Amplify. This is how the Amplify client is able to get the necessary information about your backend services.
3. It modifies the .gitignore file, adding some generated files to the ignore list
4. A cloud project is created for you in the AWS Amplify Console that can be accessed by running amplify console. The Console provides a list of backend environments, deep links to provisioned resources per Amplify category, status of recent deployments, and instructions on how to promote, clone, pull, and delete backend resources


Install Amplify Libraries
The aws-amplify package is the main library for working with Amplify Libraries in your projects:

```console
npm install aws-amplify
```
5. Set up frontend

Next, configure Amplify so it can interact with backend services.

```javascript
import { Amplify } from 'aws-amplify';
import awsExports from './aws-exports';
Amplify.configure(awsExports);


```

And that's all it takes to configure Amplify. As you add or remove categories and make updates to your backend configuration using the Amplify CLI, the configuration in aws-exports.js will update automatically.

Now that your React app is set up and Amplify is initialized, you can add an API in the next step.

6. Connect API and database to the app

Now that you’ve created and configured a React app and initialized a new Amplify project, you can add a feature. The first feature you will add is an API.

The Amplify CLI supports creating and interacting with two types of API categories: REST and GraphQL.

The API you will be creating in this step is a GraphQL API using AWS AppSync (a managed GraphQL service) and the database will be Amazon DynamoDB (a NoSQL database).

Create a GraphQL API and database

```console
amplify add api
```

Accept the default values which are highlighted below:

? Select from one of the below mentioned services: GraphQL
? Here is the GraphQL API that we will create. Select a setting to edit or continue Continue
? Choose a schema template: Single object with fields (e.g., “Todo” with ID, name, description).
The CLI should open this GraphQL schema in your text editor.

```javasc
type Todo @model {
  id: ID!
  name: String!
  description: String
}
```

The schema generated is for a Todo app. You'll notice a directive on the Todo type of @model. This directive is part of the GraphQL transform library of Amplify.

The GraphQL Transform Library provides custom directives you can use in your schema that allow you to do things like define data models, set up authentication and authorization rules, configure serverless functions as resolvers, and more.

A type decorated with the @model directive will scaffold out the database table for the type (Todo table), the schema for CRUD (create, read, update, delete) and list operations, and the GraphQL resolvers needed to make everything work together.

From the command line, press enter to accept the schema and continue to the next steps.

Deploying the API
To deploy this backend, run the push command:

```json

amplify push
```

? Are you sure you want to continue? Y

# You will be walked through the following questions for GraphQL code generation
? Do you want to generate code for your newly created GraphQL API? Y
? Choose the code generation language target: javascript
? Enter the file name pattern of graphql queries, mutations and subscriptions: src/graphql/**/*.js
? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions? Y
? Enter maximum statement depth [increase from default if your schema is deeply nested]: 2

? Are you sure you want to continue? Yes

...

? Do you want to generate code for your newly created GraphQL API Yes
? Choose the code generation language target javascript
? Enter the file name pattern of graphql queries, mutations and subscriptions src/graphql/**/*.js
? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions Yes
? Enter maximum statement depth [increase from default if your schema is deeply nested] 2



Now the API is live and you can start interacting with it!

The API you have deployed is for a Todo app, including operations for creating, reading, updating, deleting, and listing todos.

Next, run the following command to check Amplify's status:

```console
amplify status
```
This will give us the current status of the Amplify project, including the current environment, any categories that have been created, and what state those categories are in. It should look similar to this:

Current Environment: dev

| Category | Resource name | Operation | Provider plugin   |
| -------- | ------------- | --------- | ----------------- |
| Api      | myapi         | No Change | awscloudformation |

To view the GraphQL API in the AppSync console at any time, run the following command:

Try running a couple of mutations locally and then querying for the todos:

```javascript
mutation createTodo {
  createTodo(input: {
    name: "Build an API"
    description: "Build a serverless API with Amplify and GraphQL"
  }) {
    id
    name
    description
  }
}

query listTodos {
  listTodos {
    items {
      id
      description
      name
    }
  }
}
```

## Connect frontend to API

In this section you will create a way to list and create todos from the React application. To do this, you will create a form with a button to create todos as well as a way to fetch and render the list of todos.



```python
import React, { useEffect, useState } from 'react';
import { Amplify, API, graphqlOperation } from 'aws-amplify';
import { createTodo } from './graphql/mutations';
import { listTodos } from './graphql/queries';

import awsExports from "./aws-exports";
Amplify.configure(awsExports);
const initialState = { name: '', description: '' }

const App = () => {
  const [formState, setFormState] = useState(initialState)
  const [todos, setTodos] = useState([])

  useEffect(() => {
    fetchTodos()
  }, [])

  function setInput(key, value) {
    setFormState({ ...formState, [key]: value })
  }

  async function fetchTodos() {
    try {
      const todoData = await API.graphql(graphqlOperation(listTodos))
      const todos = todoData.data.listTodos.items
      setTodos(todos)
    } catch (err) { console.log('error fetching todos') }
  }

  async function addTodo() {
    try {
      if (!formState.name || !formState.description) return
      const todo = { ...formState }
      setTodos([...todos, todo])
      setFormState(initialState)
      await API.graphql(graphqlOperation(createTodo, {input: todo}))
    } catch (err) {
      console.log('error creating todo:', err)
    }
  }
  return (
# html code is below
  )
}
const styles = {
  container: { width: 400, margin: '0 auto', display: 'flex', flexDirection: 'column', justifyContent: 'center', padding: 20 },
  todo: {  marginBottom: 15 },
  input: { border: 'none', backgroundColor: '#ddd', marginBottom: 10, padding: 8, fontSize: 18 },
  todoName: { fontSize: 20, fontWeight: 'bold' },
  todoDescription: { marginBottom: 0 },
  button: { backgroundColor: 'black', color: 'white', outline: 'none', fontSize: 18, padding: '12px 0px' }
}

export default App


```

`

    <div style={styles.container}>
      <h2>Amplify Todos</h2>
      <input
        onChange={event => setInput('name', event.target.value)}
        style={styles.input}
        value={formState.name}
        placeholder="Name"
      />
      <input
        onChange={event => setInput('description', event.target.value)}
        style={styles.input}
        value={formState.description}
        placeholder="Description"
      />
      <button style={styles.button} onClick={addTodo}>Create Todo</button>
      {
        todos.map((todo, index) => (
          <div key={todo.id ? todo.id : index} style={styles.todo}>
            <p style={styles.todoName}>{todo.name}</p>
            <p style={styles.todoDescription}>{todo.description}</p>
          </div>
        ))
      }
    </div>
    
    
    `



## Add authentication

Authentication with Amplify

Amplify uses Amazon Cognito as the main authentication provider. Amazon Cognito is a robust user directory service that handles user registration, authentication, account recovery & other operations. In this tutorial, you'll learn how to add authentication to your application using Amazon Cognito and username/password login.

Create authentication service
To add authentication to your app, run this command:


```console
amplify add auth
```

To deploy the service, run the push command:

```console
amplify push
```

Now, the authentication service has been deployed and you can start using it. To view the deployed services in your project at any time, go to Amplify Console by running the following command:

```javascript
amplify console
```
</div>