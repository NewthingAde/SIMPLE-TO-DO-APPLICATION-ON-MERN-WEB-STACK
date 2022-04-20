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

- Create a pair Key as the EC2 is created ( You can call the key pair LEMP_Project)

- Move into the folder where the pair key is downloaded and run the following command to first change the mode

                                       sudo chmod 0400 LEMP_Project.pem

- Use the command to connect to the instances

                                     ssh -i LEMP_Project.pem ubuntu@<Public-IP-address>
                                     
