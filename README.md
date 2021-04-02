# Dockerizing a Node.js web app

The goal of this example is to show you how to get a Node.js application into a Docker container which is only intended for development, and not for a production deployment. We will create a simple web application in Node.js, then we will build a Docker image for that application, and lastly we will instantiate a container from that image.

#Create the Node.js app

First, create a new directory where all the files would live. In this directory create a package.json file that describes your app and its dependencies:

![image](https://user-images.githubusercontent.com/33059878/113434671-fd4e7900-9413-11eb-80db-5ce216074937.png)

With your new package.json file, run npm install. If you are using npm version 5 or later, this will generate a package-lock.json file which will be copied to your Docker image.

Then, create a server.js file that defines a web app using the Express.js framework:
