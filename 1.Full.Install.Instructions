# Lesson 1 - Full Setup Instructions
1) Create the project 

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition magento-ce'

2) Add the Magento Cloud Docker Repository and ECE Tools

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer config repositories.mcd vcs git@github.com:magento/magento-cloud-docker.git'

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer config repositories.et vcs git@github.com:magento/ece-tools.git'

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer require "magento/magento-cloud-docker:1.1.x-dev as 1.0.0" "magento/ece-tools:dev-develop"'

3) Copy files from https://github.com/magento/magento-cloud

       .magento/ (entire folder)
       .magento.app.yaml
       magento-vars.php
       php.ini

4) Create the docker-compose config and bring up instances

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=developer"
       docker-compose up -d

5) Optionally, add sample data

       docker-compose run deploy bin/magento sampledata:deploy

6) Deploy and Automatically Install

       docker-compose run deploy cloud-deploy

