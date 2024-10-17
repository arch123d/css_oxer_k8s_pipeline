# Use the official Nginx Alpine image for a lightweight image
FROM nginx
# Copy the static HTML files and other necessary files to the Nginx directory
COPY . /usr/share/nginx/html/
# Expose port 80 to allow external access
EXPOSE 80
# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
