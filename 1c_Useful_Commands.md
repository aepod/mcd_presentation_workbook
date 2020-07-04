# Lesson 1 - Useful Commands

### Without docker-compose containers running

1) Composer Install

       docker run -it  -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer install'

2) ECE-Tools from vendor/bin/

       docker run -it  -v $(pwd):/app/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'vendor/bin/ece-tools'

### After containers are running

1) Composer Install

       docker-compose run deploy 'composer install'

2) bin/magento command

       docker-compose run deploy 'bin/magento'

3) Get a Bash Shell

       docker-compose run deploy bash

4) Deploy Magento

       docker-compose run deploy cloud-deploy
