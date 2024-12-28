# Step 1: Build the React app
FROM node:18 AS build

WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy application code
COPY . .

# Build the React app for production (this generates the build/ folder)
RUN npm run build

# Step 2: Set up Nginx to serve the app
FROM nginx:alpine

# Copy the build output to Nginx's public directory
COPY --from=build /app/build /usr/share/nginx/html

# Change the default port to 8080 (Cloud Run's expected port)
RUN sed -i 's/80/8080/g' /etc/nginx/conf.d/default.conf

# Expose port 8080
EXPOSE 8080

# Run the Nginx server
CMD ["nginx", "-g", "daemon off;"]
