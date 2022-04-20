# SIMPLE-TO-DO-APPLICATION-ON-MERN-WEB-STACK

This Project is to implement a web solution based on MERN stack in AWS Cloud.

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

- Next, Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:

                                http://<PublicIP-or-PublicDNS>:5000
                                
Quick reminder how to get your server’s Public IP and public DNS name:
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

- Next, we change directory into the newly created ‘models’ folder with
                                        
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
                                                        

- Next, we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

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

- You should test all the API endpoints and make sure they are working. For the endpoints that require body, you should send JSON back with the necessary fields since it’s what we setup in our code.

- Next, open your Postman, create a POST request to the API
        
- This request sends a new task to our To-Do list so the application could store it in the database.
                                
                                        http://<PublicIP-or-PublicDNS>:5000/api/todos. 
        
<img width="1438" alt="Screenshot 2022-04-20 at 15 53 50" src="https://user-images.githubusercontent.com/80678596/164247400-2778f641-9f4e-4d3d-86df-9c6691ec43cd.png">
        

