# Docker-php-fpm

This project is a docker-compose boilerplate to help you launch a PHP application fast. This small docker compose stack will launch the latest php-fpm, in combination with the latest nginx, both runnning on alpine.

### Launch your server

* Clone the project to us as your web server.
* Add a .env file in your project. The ${SOURCE_FOLDER} variable should point to your php application folder path.
* Add the following entry to your hosts file `127.0.0.1 php-docker.local`
* Enter `php-docker.local:8080` to reach your website
*`php-docker.local` is arbitrary, (@see nginx/site.conf)*

### Additionnal tips
* Since we will be using docker volumes, we need to change permissions for the application code to match the with the docker container user. _The GID 2048 is arbitrary, this is the group I chose to run the php-fpm container. See the Dockerfile.  (Go read Niels Søholm [article](https://medium.com/@nielssj/docker-volumes-and-file-system-permissions-772c1aee23ca)) if you want to know more about volumes and permissions_
```sh
sudo chown -R ${MYUSER}:2048 ${SOURCE_FOLDER}
sudo find ${SOURCE_FOLDER} -type f -exec chmod 664 {} \;
sudo find ${SOURCE_FOLDER} -type d -exec chmod 775 {} \; 
```

* To run composer from a container; run this in your ${SOURCE_FOLDER}
```sh
docker run --rm -v $(pwd):/app composer install
```
