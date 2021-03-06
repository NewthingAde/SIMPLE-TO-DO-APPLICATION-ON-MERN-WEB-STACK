# SIMPLE-TO-DO-APPLICATION-ON-MERN-WEB-STACK

This Project is to implement a web solution based on MERN stack in AWS Cloud. MERN (MongoDB, ExpressJS, ReactJS, NodeJS)


- ### MERN Web stack consists of following components:

        MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

        ExpressJS: A server side Web Application framework for Node.js.

        ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

        Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

<img width="638" alt="MERN-stack" src="https://user-images.githubusercontent.com/80678596/164201618-f06a3f9e-0f46-4f9a-8638-c5287ecd6002.png">

## CREATING EC2 INSTANCE ON AWS

- Select region (the cl and launch a new EC2 instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM)

- Create a pair Key as the EC2 is created ( You can call the key pair MERN_Project)

- Move into the folder where the pair key is downloaded and run the following command to first change the mode

                                       sudo chmod 0400 MERN_Project.pem

- Use the command to connect to the instances

                                     ssh -i MERN_Project.pem ubuntu@<Public-IP-address>
                                     
## BACKEND CONFIGURATION

- Update ubuntu using this command line 

                                        sudo apt update

- Upgrade ubuntu using the command line 

                                         sudo apt upgrade
                                         
                                         
- Next, get the location of Node.js software from Ubuntu repositories. 

                                    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -                                     
                                         
- Next, we Install Node.js into the server with the command below       
                                         
                                     sudo apt-get install -y nodejs
                                    
-  The above command have installs both nodejs and npm. The NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts. Now we will verify the installation of Node and NPM

- Verify the installation of Node 
                                        
                                        node -v 
- Verify the installation of NPM
                                         
                                         npm -v 
                                         
- Next, we create a new directory for the To-Do project

                                         mkdir Todo
                                         
- We can check what we have in our directory with this command

                                                ls          
                                                
- Next we will move into the new directory we just created 

                                                cd Todo

- Next we will initialise the project using the command npm init so that a new file named package.json will be created. We can press Enter key to accept default and finally yes to accept the configuaration.

                                                  npm init

<img width="573" alt="Screenshot 2022-04-20 at 12 56 39" src="https://user-images.githubusercontent.com/80678596/164216465-78f53bdf-c4a1-4e9e-8e52-a00c6a36776a.png">

- Next, we run the command ls to confirm that you have package.json file created.

                                                ls
                                          
## INSTALL EXPRESSJS

Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.

- We use express by installing it using npm

                                                npm install express
                                                
<img width="636" alt="Screenshot 2022-04-20 at 13 04 41" src="https://user-images.githubusercontent.com/80678596/164217396-d291965f-0a56-417a-9b8c-94a4907d125d.png">

- Next, we create a file index.js with the command below

                                touch index.js
- Run ls to confirm that your index.js file is successfully created. ( You will see the following in the directory index.js, node_modules  package-lock.json, package.json)

                                        ls    
                                        
- Next we will install dotenv module        

                                                npm install dotenv
                                                
- Next we open the index.js file with the command line below 

                                                vim index.js
                                                
- Next, copy and paste the code into the open file and save it. (Use :w to save in vim and use :qa to exit vim)

                                const express = require('express');
                                require('dotenv').config();

                                const app = express();

                                const port = process.env.PORT || 5000;

                                app.use((req, res, next) => {
                                res.header("Access-Control-Allow-Origin", "\*");
                                res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
                                next();
                                });

                                app.use((req, res, next) => {
                                res.send('Welcome to Express');
                                });

                                app.listen(port, () => {
                                console.log(`Server running on port ${port}`)
                                });
                                                
 - Next we start our server to see that it works 

                                                node index.js
                                                
- If every thing goes well, you should see Server running on port 5000 in your terminal.

<img width="382" alt="Screenshot 2022-04-20 at 13 15 44" src="https://user-images.githubusercontent.com/80678596/164219120-41ce0fee-52c8-4024-8ddf-8ad730bb9074.png">

- Now we need to open this port in EC2 Security Groups and open port 5000

- Next, Open up your browser and try to access your server???s Public IP or Public DNS name followed by port 5000:

                                http://<PublicIP-or-PublicDNS>:5000
                                
Quick reminder how to get your server???s Public IP and public DNS name:
1) You can find it in your AWS web console in EC2 details
2) Run curl -s http://169.254.169.254/latest/meta-data/public-ipv4 for Public IP address or curl -s http://169.254.169.254/latest/meta-data/public-hostname for Public DNS name.

<img width="506" alt="Screenshot 2022-04-20 at 13 20 22" src="https://user-images.githubusercontent.com/80678596/164220538-171a10ce-4960-46b7-8b16-502caf3408e2.png">

<img width="592" alt="Screenshot 2022-04-20 at 13 22 13" src="https://user-images.githubusercontent.com/80678596/164220581-85b02887-1a21-4573-b67a-e080f1d332d1.png">

## CREATING ROUTES

There are three actions that our To-Do application needs to be able to do:

1. Create a new task
2. Display list of all tasks
3. Delete a completed task

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

- For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes

                                            mkdir routes
                                            
- Change directory to routes folder.

                                               cd routes
                                               
- Next, create a file api.js with the command below

                                                touch api.js

- Open the api.js file you just with the command below

                                                vim api.js
                                          
- copy and paste the folllowing command in the api.js file. USe :w to save it and :q to exit

                                const express = require ('express');

                                const router = express.Router();

                                router.get('/todos', (req, res, next) => {

                                });

                                router.post('/todos', (req, res, next) => {

                                });

                                router.delete('/todos/:id', (req, res, next) => {

                                })

                                module.exports = router;


## MODELS

Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model. A model is at the heart of JavaScript based applications, and it is what makes it interactive.

- To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

- Next we are going to install Mongoose but before that we need to change the directory back to Todo and then from there we install the package 

                                                cd .. 
                                        
- We install Mongoose using the command below 

                                              npm install mongoose

- Create a new folder models

                                                mkdir models

- Next, we change directory into the newly created ???models??? folder with
                                        
                                                cd models
                                                
- Inside the models folder, create a file and name it todo.js

                                                touch todo.js

Note: You can use the command below at once 

                                                mkdir models && cd models && touch todo.js
                                                
- Open the file created with vim todo.js then paste the code below in the file

                                                vim todo.js
                                                
- Copy and paste the command below into the open todo.js file

                                        const mongoose = require('mongoose');

                                        const Schema = mongoose.Schema;

                                        //create schema for todo
                                        const TodoSchema = new Schema({
                                        action: {
                                        type: String,
                                        required: [true, 'The todo text field is required']
                                        }
                                        })

                                        //create model for todo
                                        const Todo = mongoose.model('todo', TodoSchema);

                                        module.exports = Todo;
                                                        

- Next, we need to update our routes from the file api.js in ???routes??? directory to make use of the new model.

- In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit

                                const express = require ('express');
                                const router = express.Router();
                                const Todo = require('../models/todo');

                                router.get('/todos', (req, res, next) => {

                                //this will return all the data, exposing only the id and action field to the client
                                Todo.find({}, 'action')
                                .then(data => res.json(data))
                                .catch(next)
                                });

                                router.post('/todos', (req, res, next) => {
                                if(req.body.action){
                                Todo.create(req.body)
                                .then(data => res.json(data))
                                .catch(next)
                                }else {
                                res.json({
                                error: "The input field is empty"
                                })
                                }
                                });

                                router.delete('/todos/:id', (req, res, next) => {
                                Todo.findOneAndDelete({"_id": req.params.id})
                                .then(data => res.json(data))
                                .catch(next)
                                })

                                module.exports = router;
                                                        
## MONGODB DATABASE

We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up with this https://www.mongodb.com/. Follow the sign up process, select AWS as the cloud provider, and choose a region near you.

- In the index.js file, we specified process.env to access environment variables, but we have not yet created this file. So we need to do that now.
- Create a file in your Todo directory and name it .env.

                                                touch .env
                                                vi .env
- Add the connection string to access the database in it, just as below:

                           DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
Note: Ensure to update <username>, <password>, <network-address> and <database> according to your setup

- Now we need to update the index.js to reflect the use of .env so that Node.js can connect to the database.

- Open the file with vim index.js

- Now, paste the entire code below in the file
                                
                                const express = require('express');
                                const bodyParser = require('body-parser');
                                const mongoose = require('mongoose');
                                const routes = require('./routes/api');
                                const path = require('path');
                                require('dotenv').config();

                                const app = express();

                                const port = process.env.PORT || 5000;

                                //connect to the database
                                mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
                                .then(() => console.log(`Database connected successfully`))
                                .catch(err => console.log(err));

                                //since mongoose promise is depreciated, we overide it with node's promise
                                mongoose.Promise = global.Promise;

                                app.use((req, res, next) => {
                                res.header("Access-Control-Allow-Origin", "\*");
                                res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
                                next();
                                });

                                app.use(bodyParser.json());

                                app.use('/api', routes);

                                app.use((err, req, res, next) => {
                                console.log(err);
                                next();
                                });

                                app.listen(port, () => {
                                console.log(`Server running on port ${port}`)
                                });

- Next, we start your server using the command
                                                
                                                        node index.js
- You shall see a message below
        
<img width="542" alt="Screenshot 2022-04-20 at 15 26 22" src="https://user-images.githubusercontent.com/80678596/164240910-65acc636-3842-4e18-8130-a2528487d785.png">
        
So far we have written backend part of our To-Do application, and configured a database, but we do not have a frontend UI yet. We need ReactJS code to achieve that. But during development, we will need a way to test our code using RESTfulL API. Therefore, we will need to make use of some API development client to test our code.

- Next, we will use Postman to test our API.
        
- You can download and install postman on your machine or use it online.

- You should test all the API endpoints and make sure they are working. For the endpoints that require body, you should send JSON back with the necessary fields since it???s what we setup in our code.

- Next, open your Postman, create a POST request to the API
        
- This request sends a new task to our To-Do list so the application could store it in the database.
                                
                                        http://<PublicIP-or-PublicDNS>:5000/api/todos. 
        
<img width="1438" alt="Screenshot 2022-04-20 at 15 53 50" src="https://user-images.githubusercontent.com/80678596/164247400-2778f641-9f4e-4d3d-86df-9c6691ec43cd.png">
        
## FRONTEND CREATION

Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.
        
- In the same root directory as your backend code, which is the Todo directory, we will run the following command 
                                
                                         npx create-react-app client
        
- This will create a new folder in your Todo directory called client, where you will add all the react code.

- Next, we Install concurrently. It is used to run more than one command simultaneously from the same terminal window.
        
                                                npm install concurrently --save-dev
        
- Next, we Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
        
                                                        npm install nodemon --save-dev

- In Todo folder open the package.json file. Change only the script session of the file and replace with the code below.
        
                                "scripts": {
                                "start": "node index.js",
                                "start-watch": "nodemon index.js",
                                "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
                                },
        
- Next, Change directory to ???client???
                        
                                        cd client
        
- Next, Open the package.json file
        
                                        vi package.json
        
- Add the key value pair in the package.json file 
        
                                        "proxy": "http://localhost:5000",
        
- Now, go back inside the Todo directory, and simply do:
        
                                        npm dev run
        
- Your app should open and start running on localhost:3000
        
Important note: In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2 by adding a new Security Group rule. You already know how to do it.

<img width="1352" alt="Screenshot 2022-04-20 at 17 01 08" src="https://user-images.githubusercontent.com/80678596/164261315-27ade616-c093-4f10-a7c8-e4f5f52e87c5.png">

### Creating your React Components

- From your Todo directory run
                                
                                        cd client
        
- move to the src directory
                                
                                        cd src
        
- Inside your src folder create another folder called components
        
                                        mkdir components
        
- Move into the components directory with

                                        cd components
        
- Inside ???components??? directory create three files Input.js, ListTodo.js and Todo.js.
        
                                        touch Input.js ListTodo.js Todo.js

- Open Input.js file
        
                                        - vi Input.js
        
- Copy and paste the following
        
                                import React, { Component } from 'react';
                                import axios from 'axios';

                                class Input extends Component {

                                state = {
                                action: ""
                                }

                                addTodo = () => {
                                const task = {action: this.state.action}

                                    if(task.action && task.action.length > 0){
                                      axios.post('/api/todos', task)
                                        .then(res => {
                                          if(res.data){
                                            this.props.getTodos();
                                            this.setState({action: ""})
                                          }
                                        })
                                        .catch(err => console.log(err))
                                    }else {
                                      console.log('input field required')
                                    }

                                }

                                handleChange = (e) => {
                                this.setState({
                                action: e.target.value
                                })
                                }

                                render() {
                                let { action } = this.state;
                                return (
                                <div>
                                <input type="text" onChange={this.handleChange} value={action} />
                                <button onClick={this.addTodo}>add todo</button>
                                </div>
                                )
                                }
                                }

                                export default Input
        
- move back twice to the client folder and Install Axios
        
                                                npm install axios
        
- Go to ???components??? directory
        
                                cd src/components
        
- After that open your ListTodo.js
                
                                vi ListTodo.js
        
- in the ListTodo.js copy and paste the following code
                
                        import React from 'react';

                        const ListTodo = ({ todos, deleteTodo }) => {

                        return (
                        <ul>
                        {
                        todos &&
                        todos.length > 0 ?
                        (
                        todos.map(todo => {
                        return (
                        <li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
                        )
                        })
                        )
                        :
                        (
                        <li>No todo(s) left</li>
                        )
                        }
                        </ul>
                        )
                        }

                        export default ListTodo

        
- Then in your Todo.js file you write the following code
        
                                import React, {Component} from 'react';
                                import axios from 'axios';

                                import Input from './Input';
                                import ListTodo from './ListTodo';

                                class Todo extends Component {

                                state = {
                                todos: []
                                }

                                componentDidMount(){
                                this.getTodos();
                                }

                                getTodos = () => {
                                axios.get('/api/todos')
                                .then(res => {
                                if(res.data){
                                this.setState({
                                todos: res.data
                                })
                                }
                                })
                                .catch(err => console.log(err))
                                }

                                deleteTodo = (id) => {

                                    axios.delete(`/api/todos/${id}`)
                                      .then(res => {
                                        if(res.data){
                                          this.getTodos()
                                        }
                                      })
                                      .catch(err => console.log(err))

                                }

                                render() {
                                let { todos } = this.state;

                                    return(
                                      <div>
                                        <h1>My Todo(s)</h1>
                                        <Input getTodos={this.getTodos}/>
                                        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
                                      </div>
                                    )

                                }
                                }

                                export default Todo;

- We need to make little adjustment to our react code. Delete the logo and adjust our App.js to look like this. Move to the src folder
        
                                cd ..
        
- Make sure that you are in the src folder and run
        
                                vi App.js
        
- Copy and paste the code below into it
        
                        import React from 'react';

                        import Todo from './components/Todo';
                        import './App.css';

                        const App = () => {
                        return (
                        <div className="App">
                        <Todo />
                        </div>
                        );
                        }

                        export default App;

- In the src directory open the App.css
        
                        vi App.css
        
- Then paste the following code into App.css
        
                                .App {
                                text-align: center;
                                font-size: calc(10px + 2vmin);
                                width: 60%;
                                margin-left: auto;
                                margin-right: auto;
                                }

                                input {
                                height: 40px;
                                width: 50%;
                                border: none;
                                border-bottom: 2px #101113 solid;
                                background: none;
                                font-size: 1.5rem;
                                color: #787a80;
                                }

                                input:focus {
                                outline: none;
                                }

                                button {
                                width: 25%;
                                height: 45px;
                                border: none;
                                margin-left: 10px;
                                font-size: 25px;
                                background: #101113;
                                border-radius: 5px;
                                color: #787a80;
                                cursor: pointer;
                                }

                                button:focus {
                                outline: none;
                                }

                                ul {
                                list-style: none;
                                text-align: left;
                                padding: 15px;
                                background: #171a1f;
                                border-radius: 5px;
                                }

                                li {
                                padding: 15px;
                                font-size: 1.5rem;
                                margin-bottom: 15px;
                                background: #282c34;
                                border-radius: 5px;
                                overflow-wrap: break-word;
                                cursor: pointer;
                                }

                                @media only screen and (min-width: 300px) {
                                .App {
                                width: 80%;
                                }

                                input {
                                width: 100%
                                }

                                button {
                                width: 100%;
                                margin-top: 15px;
                                margin-left: 0;
                                }
                                }

                                @media only screen and (min-width: 640px) {
                                .App {
                                width: 60%;
                                }

                                input {
                                width: 50%;
                                }

                                button {
                                width: 30%;
                                margin-left: 10px;
                                margin-top: 0;
                                }
                                }

- In the src directory open the index.css
        
                                vim index.css
        
- Copy and paste the code below
        
                                body {
                                margin: 0;
                                padding: 0;
                                font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
                                "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
                                sans-serif;
                                -webkit-font-smoothing: antialiased;
                                -moz-osx-font-smoothing: grayscale;
                                box-sizing: border-box;
                                background-color: #282c34;
                                color: #787a80;
                                }

                                code {
                                font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
                                monospace;
                                }
        
- Go to the Todo directory, When you are in the Todo directory run
        
                                npm run dev
        
