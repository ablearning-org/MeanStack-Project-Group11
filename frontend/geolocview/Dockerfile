# Stage 1: Compile and Build angular app

# Use official node image as the base image
FROM node:16 as build

# Set the working directory
WORKDIR /usr/local/app

# Add the source code to app
COPY ./ /usr/local/app/

# Install all the dependencies
RUN npm install

# Generate the build of the application
RUN npm run build

# Stage 2: Serve app with nginx server

# Use official nginx image as the base image
FROM nginx:latest

# Copy the custom default.conf
COPY default.conf /etc/nginx/conf.d/

# Copy the build output to replace the default nginx contents.
COPY --from=build /usr/local/app/dist/geolocview /usr/share/nginx/html

# Expose port 8080
EXPOSE 8080

# Start nginx server
CMD ["nginx", "-g", "daemon off;"]
