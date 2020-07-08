# Lab 3 - Changing Elasticsearch Version

### Changing Version in Docker Compose

Change the version using the build:compose command

      docker run -it  -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=developer --es 7.5"
      
Restart the containers

      docker-compose down && docker-compose up -d
      
Redeploy Application
      
      docker-compose run deploy cloud-deploy

##### Make Elasticsearch Port available to local browser      
Add a docker-compose.override.yml file to the root directory of the project. 
    
    elasticsearch:
      ports:
        - 9200:9200

Apply the configuration

      docker-compose up -d
     
     
##### View the elasticsearch config in a browser

View the config at the following URL

       http://magento2.docker:9200/
