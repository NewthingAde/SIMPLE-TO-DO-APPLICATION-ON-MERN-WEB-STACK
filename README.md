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



