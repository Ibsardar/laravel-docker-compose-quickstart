# laravel-docker-compose-quickstart (quickdrop)
 Sets up a full LAMP (LEMP NOT WORKING... DON'T DROP NGINX FOLDER INTO YOUR DIRECTORY) stack with docker-compose into your Laravel project
 
### For Nginx:
Nginx isn't working here correctly.

For a Dockerized, SSL automated, nginx quickdrop, see: https://github.com/Ibsardar/docker-compose-nginx-fpm-certbot-quickstart

For a Dockerized, SSL Automated, LEMP stack quickdrop... well it is coming soon.

### How to use:
Drop the contents of 'drop-into-your-project (apache, NOT nginx)' into your Laravel project.

You can edit as you like. These are the files you will most likely be editing after the drop:
- server/.env
- server/init.sh
- server/init.sql
- server/vhost.conf
- dockerfiles/webserver.Dockerfile
- .gitignore

### Quickstart:
Login to your server.

Pull your project (after the drop above) onto the server.

Navigate to your project's main directory.

Run `docker-compose build && docker-compose up`

### Security & Other Common Edits:
***(do the following before running docker-compose build)***

Login to your server.

Navigate to your project's main directory.

Edit the following files:


File | Detail | Example | Security
--- | --- | --- | ---
server/.env | "APP_NAME" | *MyBlog* | no
server/.env | "APP_ENV" | *taging, production* | no
server/.env | "APP_DEBUG" | *true, false* | no
server/.env | "APP_URL" | *http://localhost:123, https://www.myblog.com* | no
server/.env | "DB_DATABASE" | *blog_database* | no
server/.env | "DB_USERNAME" | jdoe | **YES**
server/.env | "DB_PASSWORD" | pAsSwOrD123 | **YES**
server/init.sql | Replace "my_default_db" | *blog_database* | no
server/vhost.conf | "ServerName" | *www.example.com* | no
server/vhost.conf | "ServerAdmin" | *someones@email.com* | no
server/vhost.conf | Uncomment "SSL..." and edit to enable https** | *...* | **YES**
.gitignore | ... | *...* | no
docker-compose.yml | Change port numbers "81", "444", "3307", and "8000" to the ports you want to use *(make sure server/.env > APP_URL is updated to use correct port)* | *3307:3306 i.e. \<**HOST SERVER PORT**\>:\<**CONTAINER SERVER PORT**\>* | **YES**
docker-compose.yml | Change volume locations on the host server so they do not conflict with other running docker-compositions on the same host server | */docker/\<**MY_PROJECT**\>/volumes/mysql:/var/lib/mysql* | no
dockerfiles/webserver.Dockerfile | Add under "# php 7.4" | *RUN apt-get -y install php7.4-**\<A NEEDED MISSING PHP PKG\>*** | no

### Troubleshoot:
Run `docker-compose config --services` to check the names of services.

Run `docker-compose ps` to check the status of the services.

Run `docker container ls` to check the status of the containers.

Run `docker-compose exec <SERVICE_NAME> bash` to enter into an up and running service for further investigation.

Run `docker-compose build --no-cache && docker-compose up` to rebuild everything from scratch.
