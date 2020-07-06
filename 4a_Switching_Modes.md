# Lesson 4 - Switching Modes

### Production Mode

1) Ensure containers are down

       docker-compose down -v

2) Switch to production mode

       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=production"

3) Start Containers

       docker-compose up -d
       
4) Build / Deploy / Post-Deploy

       docker-compose run build cloud-build
       docker-compose run deploy cloud-deploy
       docker-compose run deploy cloud-post-deploy

5) (optional) Enable Varnish

       docker-compose run deploy magento-command config:set system/full_page_cache/caching_application 2 --lock-env
       docker-compose run deploy magento-command setup:config:set --http-cache-hosts=varnish

6) Clear Cache

       docker-compose run deploy magento-command cache:clean
       
7) If Static Content is broken, you may have to restart containers

       docker-compose run deploy magento-command clean:cache  
       
Site should be working in production mode, with most files in read-only mode.

       https://magento2.docker

---

### Development Mode

1) Ensure containers are down

       docker-compose down -v

2) Switch to development mode
       
       docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=development"
       
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