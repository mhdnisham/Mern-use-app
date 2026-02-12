# --- Stage 1: Build the application ---
FROM node:20-alpine As builder

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker cache
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Run the build command (adjust this for your framework, e.g., 'react-scripts build', 'vue-cli-service build')
RUN npm run build


# --- Stage 2: Production runtime environment (using Nginx to serve static files) ---
FROM nginx:alpine AS production


# Copy the built files from the builder stage to Nginx's serving directory
# The 'build' or 'dist' folder name depends on your project's build output
COPY --from=builder /app/build /usr/share/nginx/html

# Copy a custom nginx configuration if needed, otherwise default is fine for static sites
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80 for the Nginx server
EXPOSE 80


# The default command for nginx:alpine runs Nginx
CMD [ "nginx", "-g" , "deamon off;" ]

