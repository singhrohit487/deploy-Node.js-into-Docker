# Dockerizing a Node.js web app

The goal of this example is to show you how to get a Node.js application into a Docker container which is only intended for development, and not for a production deployment. We will create a simple web application in Node.js, then we will build a Docker image for that application, and lastly we will instantiate a container from that image.

# Create the Node.js app

First, create a new directory where all the files would live. In this directory create a package.json file that describes your app and its dependencies:

![image](https://user-images.githubusercontent.com/33059878/113434671-fd4e7900-9413-11eb-80db-5ce216074937.png)

With your new package.json file, run npm install. If you are using npm version 5 or later, this will generate a package-lock.json file which will be copied to your Docker image.

Then, create a server.js file that defines a web app using the Express.js framework:

![image](https://user-images.githubusercontent.com/33059878/113434937-71891c80-9414-11eb-81bd-ff1b9c97467f.png)

In the next steps, we'll look at how you can run this app inside a Docker container using the official Docker image. First, you'll need to build a Docker image of your app.

# Creating a Dockerfile

Create a file called Dockerfile to build the docker image. Your Dockerfile should now look like this:

![image](https://user-images.githubusercontent.com/33059878/113435226-f6743600-9414-11eb-9911-b24eaf044a80.png)

# .dockerignore file

Create a .dockerignore file in the same directory as your Dockerfile with following content:

![image](https://user-images.githubusercontent.com/33059878/113435363-3509f080-9415-11eb-86cf-8c1811a17ee3.png)

This will prevent your local modules and debug logs from being copied onto your Docker image and possibly overwriting modules installed within your image.

# Building your image

Go to the directory that has your Dockerfile and run the following command to build the Docker image. The -t flag lets you tag your image so it's easier to find later using the docker images command:

$ docker build -t <your username>/node-web-app .

# Run the image

Running your image with -d runs the container in detached mode, leaving the container running in the background. The -p flag redirects a public port to a private port inside the container. Run the image you previously built:

$ docker run -p 49160:8080 -d <your username>/node-web-app

# Get container ID

$ docker ps

# Print app output
$ docker logs <container id>

# Example
Running on http://localhost:8080

# Test

To test your app, get the port of your app that Docker mapped:

$ docker ps

In the example above, Docker mapped the 8080 port inside of the container to the port 49160 on your machine.

Now you can call your app using curl (install if needed via: sudo apt-get install curl):

![image](https://user-images.githubusercontent.com/33059878/113435856-3a1b6f80-9416-11eb-8c13-0950ae73db77.png)

I hope this helped you get up and running a simple Node.js application on Docker.
