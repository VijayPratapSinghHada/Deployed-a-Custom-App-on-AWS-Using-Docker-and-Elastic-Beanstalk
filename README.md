<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App with Docker

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eb)

**Author:** Vijay Pratap Singh Hada  
**Email:** vijaypratapsinghhada9@gmail.com

---

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eb_c4df13c84)

---

## Introducing Today's Project!

### What is Docker?

Docker is a tool that helps developers create, manage, and deploy applications using containers. In today's project, I used Docker to build a custom container image that included my web application and its dependencies. This image was then deployed on AWS Elastic Beanstalk, allowing me to run my app in a scalable, cloud environment. Docker made the process easier by ensuring my app worked consistently across different platforms. 

### One thing I didn't expect...

One thing I didn't expect in this project was how simple and easy, it was to deploy a custom image on Elastic Beanstalk, which is a Platform as a Service (PaaS). It was a new experience for me, as I learned not only how to package my application into a Docker container but also how easily Elastic Beanstalk handles the deployment and scaling of my app in the cloud. 

### This project took me...

This project took me approximately 2 hours and 10 minutes, including the time spent on documenting each step of the process. 

---

## Understanding Containers and Docker

### Containers

Containers are a standardized way to package software, including the code and all the necessary dependencies, so that applications run reliably across different computing environments. They are useful because they solve the problem of "it works on my machine," ensuring that all team members work in the same environment, even if they are using different computers. When developing complex web applications, containers help maintain consistency and make collaboration easier, allowing teams to focus on building features rather than dealing with setup issues.

A container image is a blueprint or template that contains everything needed to create a container. It tells Docker what to include in the container, such as application code, libraries, dependencies, and other necessary files. From a single container image, you can create multiple identical containers that will behave the same way no matter where they are deployed.

### Docker

Docker is a tool that helps you create, manage, and deploy containers efficiently. It packages your applications and all their dependencies into a single unit, making them easier to share and run. Docker Desktop is a program designed to make working with Docker simple and user-friendly. It allows you to build, test, and deploy applications directly from your computer. With Docker Desktop, you can easily manage your containers, monitor their performance, and adjust their settings, all from a convenient dashboard. 

The Docker daemon is a background engine that manages Docker containers, handling tasks like building, running, and distributing them. It works behind the scenes, taking commands from the Docker client is what you type in the terminal or click in Docker Desktop and performs the necessary actions. When you run a Docker command, it’s the daemon that does the actual work, allowing your applications to run smoothly. 

---

## Running an Nginx Image

Nginx is a powerful web server that serves web pages to users on the internet. It is designed to handle high levels of web traffic smoothly and efficiently, making it popular among developers. Nginx can also function as a proxy server, meaning it can forward requests from users to other servers. This helps balance the load and allows multiple users to access the website without slowing down performance. 

The command I ran to start a new container was `docker run -d -p 80:80 nginx`. This command creates a new container using a pre-existing container image called Nginx. The `-d` option means the container will run in the background, allowing other tasks to continue. The `-p 80:80` part maps port 80 on my computer to port 80 in the container, so I can access the webpage that Nginx is serving through my web browser. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eb_6245f5bb10)

---

## Creating a Custom Image

The Dockerfile is a document that contains all the instructions needed to build a Docker image. It provides Docker with details on how to set up the application environment and which software packages to install. By reading the Dockerfile, Docker learns how to create a customized container image that meets the specific needs of your application.

My Dockerfile tells Docker three things. First, the line `FROM nginx:latest` specifies that our custom image starts from the latest Nginx image, allowing us to build upon its existing features. Second, the line `COPY index.html /usr/share/nginx/html/` replaces the default HTML file with our own custom `index.html`, so the Nginx server displays our web content. Lastly, the line `EXPOSE 80` indicates that our container will receive web traffic through port 80, making it accessible for users and services to interact with our web application easily. 

The command I used to build a custom image with my Dockerfile was `docker build -t my-web-app .` The `-t my-web-app` option names my newly created image "my-web-app," while the `.` at the end of the command tells Docker to look for the Dockerfile in the current directory, which is the Compute folder. This process involves Docker reading the instructions from my Dockerfile, including copying my `index.html` file into the image, and preparing everything needed to run my web application in a container. Building the image allows me to easily deploy my application anywhere using Docker. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eb_4c741d1913)

---

## Running My Custom Image

There was an error when I ran my custom image because another container was already using port 80, preventing my new container from accessing it. The error message indicated a conflict with the network because the existing container was still active. I resolved this by checking Docker Desktop to identify the container occupying port 80, which turned out to be the Nginx container I had previously run. I then stopped that container using the stop icon and confirmed it was no longer running. After that, I successfully ran my custom image without any issues. 

In this example, the container image is the blueprint that contains all the instructions for creating the container, including the application code, dependencies, and libraries needed for the web server. It serves as a template from which multiple identical containers can be created. On the other hand, the container is the actual instance of the software that is running, serving the web content from the `index.html` file. Essentially, the container is what you interact with, while the container image is what defines how that container is built and what it contains. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eb_74b5c3d619)

---

## Elastic Beanstalk

Elastic Beanstalk is a service provided by AWS that simplifies the deployment of cloud applications. It allows developers to upload their code without needing to manage the underlying infrastructure. Elastic Beanstalk takes care of essential tasks like setting up servers, load balancing, and auto-scaling, so developers can focus on writing their application code. Additionally, Elastic Beanstalk supports applications packaged as Docker containers, making it easy to deploy containerized applications directly to the cloud. 

Deploying my custom image with Elastic Beanstalk took me about 10 minutes. During this time, I set up the application by following the steps in the Elastic Beanstalk console, including uploading my Dockerfile and HTML file as a ZIP archive. The service then handled all the necessary processes to create an environment, set up the infrastructure, and deploy my application. Once the deployment was complete, I was able to access my webpage through the provided domain link, confirming that everything was set up correctly and ready for users to view.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eb_26d5573b23)

---

## Deploying App Updates

To learn how to deploy app updates with Elastic Beanstalk, I updated my app by adding new content to my `index.html` file, including a subheading and a custom image. I included the line `<h2>And  a special image chosen by me:</h2>` followed by an `<img>` tag that links to a public image online. This enhances the appearance of my web app. I verified those changes by opening the updated `index.html` file in my web browser to ensure everything displayed correctly.

My app updates didn't show up in my live environment immediately because the changes I made to `index.html` were stored only on my local computer, while Elastic Beanstalk was still running the previous version of my app from the uploaded ZIP file. To deploy my changes, I first deleted the old ZIP file and compressed my updated `index.html` and `Dockerfile` into a new ZIP file. Then, I went back to the Elastic Beanstalk console, selected my environment, and uploaded the new ZIP file as "Version Two." This process allowed me to update the live app without repeating the entire environment setup. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eb_5b7034684)

---

---
