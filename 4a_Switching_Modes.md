# Lab 4 - Switching Modes

### Production Mode

1) Ensure containers are down

       docker-compose down -v

2) Switch to production mode

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=production"

3) Start Containers

       docker-compose up -d
       
4) Build 

Currently there is a bug in the build process, you have to manually remove the redis from the app/etc/env.php while running build. There are several copies of the env.php to allow for this in the example site. 

       cp app/etc/env.php.build app/etc/env.php
       docker-compose run build cloud-build
       cp app/etc/env.php.normal app/etc/env.php

5) Deploy / Post-Deploy

       docker-compose run deploy cloud-deploy
       docker-compose run deploy cloud-post-deploy

6) (optional) Enable Varnish

       docker-compose run deploy magento-command config:set system/full_page_cache/caching_application 2 --lock-env
       docker-compose run deploy magento-command setup:config:set --http-cache-hosts=varnish

7) Clear Cache

       docker-compose run deploy magento-command cache:clean
       
8) If Static Content is broken, you may have to restart containers

       docker-compose restart  
       
Site should be working in production mode, with most files in read-only mode.

       https://magento2.docker

---

### Development Mode

1) Ensure containers are down

       docker-compose down -v

2) Switch to development mode
       
       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=developer"
       
3) Start Containers

       docker-compose up -d
       
4) Deploy / Post-Deploy

       docker-compose run deploy cloud-deploy
       docker-compose run deploy cloud-post-deploy
       
5) (optional) Enable Varnish

       docker-compose run deploy magento-command config:set system/full_page_cache/caching_application 2 --lock-env
       docker-compose run deploy magento-command setup:config:set --http-cache-hosts=varnish
       
6) Clear Cache

       docker-compose run deploy magento-command cache:clean
       
Site should be working in development mode, with all files in read/write mode.

       https://magento2.docker