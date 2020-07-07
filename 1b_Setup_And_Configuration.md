# Lab 1 - Setup and Configuration

1)  Add `magento2.docker` hostname to your local hosts file.

    -  Docker Desktop or Linux Native: `127.0.0.1 magento2.docker`

    -  Linux VM: `{IP of VM} magento2.docker`

2)  Download project at https://bit.ly/31EwEPe
    
3)  Extract. Depending on your download and OS, extract the compressed file and change to the directory. This is just a standard Magento v2.3.5 demo data enabled installation; very vanilla.

4)  Bring up containers by running `docker-compose up -d`

5)  View website over at https://magento2.docker/
