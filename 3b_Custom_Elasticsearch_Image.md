# Lesson 2 - Custom Elasticsearch Docker Image

1) Setup custom image 

Copy the Elasticsearch 7.5 image into private directory.

       mkdir -p .docker/images/elasticsearch
       cp -R vendor/magento/magento-cloud-docker/images/elasticsearch/7.5/* .docker/images/elasticsearch/ 
       
2) Add S3 Repository Plugin to Elasticsearch

Edit `.docker/images/elasticsearch/Dockerfile`

     FROM docker.elastic.co/elasticsearch/elasticsearch:7.5.2
     
     RUN echo "xpack.security.enabled: false" >> /usr/share/elasticsearch/config/elasticsearch.yml
     RUN echo "discovery.type: single-node" >> /usr/share/elasticsearch/config/elasticsearch.yml
     RUN bin/elasticsearch-plugin install -b analysis-icu && \
         bin/elasticsearch-plugin install -b analysis-phonetic && \
         bin/elasticsearch-plugin install -b repository-s3
     
     ADD docker-healthcheck.sh /docker-healthcheck.sh
     
     HEALTHCHECK --retries=3 CMD ["bash", "/docker-healthcheck.sh"]
     
     EXPOSE 9200 9300

3) Add image override to docker-compose.override.yaml


4) Restart the service


5) Test with browser
