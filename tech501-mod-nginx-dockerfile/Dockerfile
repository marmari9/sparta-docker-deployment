# Use the official nginx base image
FROM nginx:latest

# Copy the custom index.html to the nginx web directory
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
