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


- 
