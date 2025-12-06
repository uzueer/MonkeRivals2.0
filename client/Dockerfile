# Stage 1: Build the React/Vite application
FROM node:20-alpine AS builder
WORKDIR /app
# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install
# Copy all source files
COPY . .
# Build the application (output goes to /app/dist by default for Vite)
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:stable-alpine AS production
# Copy your custom Nginx configuration file from the project root's nginx folder
# (Note: The docker-compose context is the root, so this path is relative to the root for the Nginx image)
COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf
# Copy the built static files from the 'builder' stage into the Nginx public directory
COPY --from=builder /app/dist /usr/share/nginx/html

# Nginx listens on port 80
EXPOSE 80
# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
