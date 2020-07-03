# Lesson 2 - Configuring Nginx

### Create configurations
1) Create .docker/nginx/etc directory

       mkdir -p .docker/nginx/etc directory
 
2) Copy config files from containers

Connect to the container

      docker-compose run deploy bash     

Copy the configurations from in container

      cp /etc/nginx/nginx.conf /app/.docker/nginx/etc/
      cp /etc/nginx/conf.d/default.conf /app/.docker/nginx/etc/vhost.conf
      
Don't forget to exit from the container      
      
     root@deploy:/app# exit
     [webuser@localhost magento-ce]$  
      
      
      
### Customize Configuration
We will be adding a http header that should be visible in the front-end

In .docker/nginx/etc/vhost.conf edit in the PHP Entry Point (near line 142)

      # PHP entry point for main application
      location ~ ^/(index|get|static|errors/report|errors/404|errors/503|health_check)\.php$ {
         
         # Add the following line
         add_header X-hello "Hello World";


### Restart the Web Container
Restart the nginx container

      docker-compose restart web

Clear the cache

      docker-compose run deploy bin/magento cache:flush


### Check the Configuration

Using your web browser look at the headers for any page.

Response Headers should have the following:

     X-hello: Hello World


     