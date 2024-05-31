# Use the official Node.js image as the base image
FROM node:lts-alpine as build-stage

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Install additional build tools, if necessary
RUN npm install -g serve

# Build the Vue.js application
RUN npm run build

# Use a lightweight web server to serve the static files
FROM nginx:stable-alpine as production-stage

# Copy the build output to the web server's root directory
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start the web server
CMD ["nginx", "-g", "daemon off;"]