# Lesson 2 - Configuring MySQL

### Add configuration file in  .docker/mysql/mariadb.conf.d/

Create .docker/mysql/mariadb.conf.d/lesson2.conf with the content:

      [mysqld]
      table_open_cache = 8092
      
      
### Restart the Database Container
You can just restart the Database container, if it is already running. This will reinitialize the configuration with your changes. It will not lose the database, because that is persisted in the database volume.

      docker-compose restart db



### Check the Configuration

     docker-compose run deploy bash
     
Inside the container run the following command

     mysql -u magento2 -h db -pmagento2 magento2 -e "show variables" | grep "table_open_cache"

Results will look like the following.

     root@deploy:/app# mysql -u magento2 -h db -pmagento2 magento2 -e "show variables" | grep "table_open_cache"
     table_open_cache        8092
     table_open_cache_instances      8



     