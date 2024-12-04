# Stage 1: Build the React application
FROM node:23.3.0-slim   AS builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json /app 
COPY package-lock.json /app
COPY .env /app

# Install app dependencies
RUN npm install

# Copy the current directory contents into the container
COPY public /app/public
COPY src /app/src

# Build the app
RUN npm run build

# Stage 2: Serve the React application
FROM nginx:alpine

# Copy the build output to the Nginx HTML folder
COPY --from=builder /app/build /usr/share/nginx/html

# Make port 3000 available to the world outside this container
EXPOSE 3000


# Replace the default Nginx configuration to use port 3000
RUN sed -i 's/listen       80;/listen       3000;/g' /etc/nginx/conf.d/default.conf

# Define environment variable

# Set the command to run Nginx
CMD ["nginx", "-g", "daemon off;"]