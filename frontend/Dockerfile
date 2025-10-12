# Use nginx base image
FROM nginx:alpine

# Copy all frontend files into the default nginx public folder
COPY . /usr/share/nginx/html

# Expose the port for nginx
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

