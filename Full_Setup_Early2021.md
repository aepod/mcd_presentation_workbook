# Early 20201 - Full Setup Instructions using Community Edition

This is not part of the lab, it is meant to give full reference on how the tgz file was created. 

This assumes working WSL2 or Linux docker, with php and composer installed.

1)  Create the project

        composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition magento-ce

2)  Add the Magento Cloud Docker Repository and ECE Tools

        composer require "magento/magento-cloud-docker" "magento/ece-tools"

3)  Copy files from https://github.com/magento/magento-cloud

        .magento/ (entire folder)
        .magento.app.yaml
        magento-vars.php
        php.ini

4)  Create the docker-compose config and bring up instances

        ./vendor/bin/ece-docker build:compose --sync-engine=native --mode=developer
        docker-compose up -d

5)  Optionally, add sample data

        docker-compose run deploy php -dmemory_limit=4G bin/magento sampledata:deploy

6)  Deploy and automatically install

        docker-compose run deploy cloud-deploy
        


         
