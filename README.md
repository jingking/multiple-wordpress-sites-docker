# Deploy Multiple WordPress Sites with Docker
## Introduction
This is a side project that explores the options to host multiple WordPress sites on a single server (especially with limited resources). 

This doc is a brief summary of the major steps to set up multiple WordPress sites with docker. The architecture is shown below:

<img src="illustrations/multiple-wordpress-sites-3.2.PNG" width="800" />

For single site docker deployment, see
https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-docker-compose
For overview of other Multiple WordPress sites deployment options, see notes here,  
https://github.com/jingking/multiple-wordpress-sites-docker/blob/main/deployment%20options%20for%20multiple%20wordpress%20sites.md

## Installation
- Step 1<br>
Install docker engine with compose plugin<br>
https://docs.docker.com/engine/install/

- Step 2<br>
Create work directory (e.g. wordpress) and set up folder structure with Nginx config file (http only) and .env file.<br>

- Step 3<br>
Define services with docker compose .yml file<br>
````
    cd wordpress
    sudo docker compose up
````
- Step 4<br> 
Request SSL Certificates from Letsencrypt<br>
````
    sudo docker compose -f ./docker-compose.yml -f ./docker-compose.certbot.yml run certbot
````
- Step 5<br> 
Update the Nginx configuration file (add https) and restart webserver<br>
````
    docker compose stop webserver
    docker compose up -d --force-recreate --no-deps webserver
````
- Step 6<br> 
Complet the WordPress sites installation via the browser<br>
