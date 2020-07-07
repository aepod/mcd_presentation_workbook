# Lab 4 - Generating PHP Docker Images

1) Create an ini file, disabling exec function

In `vendor/magento/magento-cloud-docker/images/php/cli/etc/` create `php-disable-functions.ini` and add the following:

      disable_functions=exec     

2) Add ini file to Dockerfiles

In `vendor/magento/magento-cloud-docker/images/php/cli/Dockerfile` add the following line around line 48.

      ADD etc/php-disable-functions.ini /usr/local/etc/php/conf.d/zz-disable-functions.ini
      
3) Generate PHP configuration

This command can be run in docker or docker-compose depending on if the containers are running. 

##### Containers Running

      docker-compose run deploy vendor/bin/ece-docker image:generate:php

##### Containers not running
      
      docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker image:generate:php"
      
4) Add override in docker-compose

       services:
           deploy:
              build:
                context: ./vendor/magento/magento-cloud-docker/images/php/7.3-cli
                

5) Rebuild containers

       docker-compose up -d --build

6) Check to see changes

        docker-compose run deploy php -i | grep disable_functions

Results should looks like:
       
       Starting magento-ce_redis_1         ... done
       Starting magento-ce_elasticsearch_1 ... done
       Starting magento-ce_db_1            ... done
       disable_functions => exec => exec

7) Revert those changes, if you don't things will be broken

       docker-compose pull
       
This command will overwrite the image that was built in step #5.