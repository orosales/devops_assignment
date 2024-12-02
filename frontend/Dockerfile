# Use an official Node runtime as a parent image
FROM node:23.3.0-slim

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json /app 
COPY package-lock.json /app

# Install app dependencies
RUN npm install

# Copy the current directory contents into the container
COPY public /app/public
COPY src /app/src

# Build the app
RUN npm run build

# Install a lightweight static file server to serve the production build
RUN npm install -g serve

# Make port 3000 available to the world outside this container
EXPOSE 3000

# Define environment variable

# Run the static server to serve the build folder
CMD ["serve", "-s", "build", "-l", "3000"]