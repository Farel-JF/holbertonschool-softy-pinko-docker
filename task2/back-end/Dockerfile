# Use the latest Nginx image as the base image
FROM nginx:latest

# Copy the softy-pinko-front-end files to the Nginx html directory
COPY ./softy-pinko-front-end /var/www/html/softy-pinko-front-end

# Copy the Nginx config file to the proper directory
COPY ./softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf
