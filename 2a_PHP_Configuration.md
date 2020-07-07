# Lab 2 - Configuring PHP

### Edit the php.ini

For instance, change the memory limit

      memory_limit = 2G   #Default is 1G
      
      
### Restart the PHP Container
You can just restart the FPM container, if it is already running. This will reinitialize the configuration with your changes.

      docker-compose restart fpm



### Check the Configuration

     docker-compose run deploy bash
     
Inside the container run the following command

     php -i | grep "memory_limit"

Results will look like the following.

     root@deploy:/app# php -i | grep "memory_limit"
     memory_limit => 2G => 2G

     