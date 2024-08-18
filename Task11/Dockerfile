# Dockerfile
# Build stage
FROM node:14 AS build

WORKDIR /app

# Clone the repository
RUN git clone https://github.com/docker/awesome-compose.git

# Navigate to the actual Angular project directory
WORKDIR /app/awesome-compose/angular/angular

# Install dependencies and build the Angular app
RUN npm install && npm run build

# Run stage
FROM nginx:stable-alpine

# Copy the build output to Nginx HTML folder
COPY --from=build /app/awesome-compose/angular/angular/dist/angular /usr/share/nginx/html

# Copy Nginx configuration file
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
