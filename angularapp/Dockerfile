# Use the official Node.js image as the base
FROM node:18 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install the project dependencies
RUN npm install

# Copy the entire project and build the application
COPY . .

# Build the Angular app
RUN npm run build

# Use the official Nginx image as the base
FROM nginx:alpine AS runtime

# Copy the built Angular app to the appropriate location
COPY --from=build /app/dist/angularapp /usr/share/nginx/html

# Expose the port your application listens on
EXPOSE 80

# Set the entry point for the container
CMD ["nginx", "-g", "daemon off;"]
