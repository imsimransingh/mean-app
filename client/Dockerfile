# Use the official Node.js image as the base image
FROM node:latest AS build

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the entire Angular project to the container
COPY . .

# Build the Angular app
RUN npm run build

# Use a smaller image for serving the app
FROM nginx:alpine

# Copy the built Angular app from the previous stage to the Nginx directory
COPY --from=build /app/dist/client /usr/share/nginx/html

# Expose port 80 for the Nginx server
EXPOSE 8080

# Start Nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]
