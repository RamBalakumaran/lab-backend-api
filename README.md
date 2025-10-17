mkdir lab-backend-api
o cd lab-backend-api
o Initialize a new Node.js project:
o npm init -y
o Install the required dependencies:
o npm install express mongoose body-parser cors
o Install nodemon as a development dependency for automatic server restarts:
o npm install --save-dev nodemon



----------------------
Step 3: Create Application File
Inside myapp/, create a file named app.py with this content:
# app.py
print("Hello from my custom Docker Image!")
Step 4: Create a Dockerfile
# Use Python base image
FROM python:3.9-slim

# Set working directory inside container
WORKDIR /app

# Copy local files into container
COPY . /app

# Run app.py when container starts
CMD ["python", "app.py"]

Step 5: Build Docker Image
docker build -t myapp:1.0 .(command promt /terminal )
Check your image:
docker images
step 6: Run and Test the Image
docker run myapp:1.0
Output should be:
Hello from my custom Docker Image!


--------------
Dockerfile:
# Stage 1: Build React app
FROM node:18 AS build

WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm install

COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:stable-alpine

# Copy React build files to Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80
# Run Nginx
CMD ["nginx", "-g", "daemon off;"]
.dockerignore:
node_modules
build
.dockerignore
Dockerfile
npm-debug.log

Steps:
Open terminal in react-demo/
Build Docker image:
	docker build -t react-demo .
Run container:
	docker run -d -p 3000:80 react-demo
Open in browser:
👉 http://localhost:3000
