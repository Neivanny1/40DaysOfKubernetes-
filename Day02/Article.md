# Day 2 of 40 Days of Kubernetes: 🚀 How To Dockerize a Project: Step-by-Step Guide 🚀 🌐☸️

<img src='./assets/2.png'>

In today’s #40DaysOfKubernetes challenge, I’ll show you how to Dockerize an application by walking through each command and its explanation. Additionally, I’ll explore the docker init command, which simplifies Dockerization, and I’ll provide a link to my GitHub repository containing the Dockerfile for reference.

Let’s get started!
## Step 1: Clone an Existing App or Use Your Own

You can either use your own application or clone a simple app from GitHub for this example. Here, I am using a sample Node.js application:
```
git clone https://github.com/docker/getting-started-app.git
```
Navigate to the project directory:
```
cd getting-started-app/
```
## Step 2: Create a Dockerfile

A Dockerfile defines the environment and commands to build and run your application inside a container. Create an empty Dockerfile in the root of your project using:
```
touch Dockerfile
```
Now, open the Dockerfile in your favorite text editor and add the following content:
```
Dockerfile

FROM node:18-alpine      # Base image: Lightweight Node.js environment
WORKDIR /app             # Set working directory to /app inside the container
COPY . .                 # Copy all project files into the container
RUN yarn install --production  # Install dependencies in production mode
CMD ["node", "src/index.js"]   # Command to run the application
EXPOSE 3000              # Expose port 3000 for external access
```
Command Explanations:
1. FROM node:18-alpine: Uses a minimal Node.js image.
2. WORKDIR /app: Sets /app as the working directory inside the container.
3. COPY . .: Copies all local project files to the container.
4. RUN yarn install --production: Installs only production dependencies.
5. CMD ["node", "src/index.js"]: Specifies the command to start the application.
6. EXPOSE 3000: Opens port 3000 to allow external traffic.

## Step 3: Build the Docker Image

With the Dockerfile ready, build the Docker image using this command:
```
docker build -t my-dockerized-app .
```
Explanation:
1. docker build: Builds a Docker image from the Dockerfile.
2. -t my-dockerized-app: Tags the image with the name "my-dockerized-app".
3. (.) : The dot indicates the current directory as the build context (where the Dockerfile is located).

Verify that the image was created by listing the images:
```
docker images
```

## Step 4: Push the Image to Docker Hub

Now that the image is built, let’s make it accessible to others by pushing it to Docker Hub. First, log in to your Docker account:
```
docker login
```
Tag the image with your Docker Hub username and repository name:
```
docker tag my-dockerized-app:latest yourusername/my-dockerized-app:latest
```
Push the image to Docker Hub:
```
docker push yourusername/my-dockerized-app:latest
```

## Step 5: Running the Docker Container

Run the container locally and expose port 3000 with this command:
```
docker run -dp 3000:3000 yourusername/my-dockerized-app:latest
```
#### Explanation:

    -d: Runs the container in detached mode (in the background).
    -p 3000:3000: Maps port 3000 on your local machine to port 3000 on the container.

Visit http://localhost:3000 in your browser to see the app running.
## Step 6: Exploring the docker init Command

Docker provides an easy way to generate Dockerfiles using the docker init command. This command analyzes your project and generates a Dockerfile automatically.

To try it out, navigate to your project directory and run:
```
docker init
```
Docker will generate a Dockerfile based on the project’s dependencies and structure. You can modify the generated Dockerfile as needed, which simplifies the process, especially for common languages like Python, Node.js, or Go.
Key Takeaways

1. Portability: Docker ensures your app runs consistently across environments.
2. Automation: The docker init command can auto-generate Dockerfiles, simplifying Dockerization for common projects.
3 Efficiency: Docker helps in streamlining application deployment and reducing setup complexity.

### GitHub Repository with Dockerfile

You can view the full project and Dockerfile in my GitHub repository:

🔗 My Dockerized App on GitHub
Sharing My Journey: https://github.com/Neivanny1/40DaysOfKubernetes-

This was an exciting and informative step in my #40DaysOfKubernetes challenge! If you're interested in containerization, give this a try and feel free to check out my repository for more examples. Big thanks to [@PiyushSachdeva](https://www.linkedin.com/in/piyush-sachdeva) and [@CloudOps Community](https://www.linkedin.com/company/thecloudopscomm) for the support.

#Docker #Kubernetes #DevOps #CloudComputing #Containerization #40DaysOfKubernetes #CKA #DockerInit