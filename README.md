GLPI server in Docker.

*****

There are 3 docker containers used to launch this GLPI server version:
* GLPI itself (NGINX, PHP v8.2, application files);
* MariaDB server;
* Adminer (database graphical control panel).

It is possible to run all containers [1] separately or [2] by using Docker Compose. See instruction below.

*****
*****

1. Run by Docker:

   docker run --name glpi-app -d -p 80:80 -p 443:443 alyonamoskalets/glpi:v1
   
   docker run --name glpi-mysql -d -p 3306:3306 -e MARIADB_USER=inventory_user -e MARIADB_PASSWORD=pass4DB -e MARIADB_DATABASE=inventory -e MARIADB_ROOT_PASSWORD=pass4Admin -e MARIADB_PORT_NUMBER=3306 -v /glpi/db:/var/lib/mysql mariadb
   
   docker run --name glpi-adminer -d -p 8080:8080 --link glpi-mysql adminer

2. Run by Docker Compose:

   docker compose up -d -f docker-compose-public.yml

*****
*****

If you would like to build GLPI Docker image by yourself from my sources, you can use do this by [1] Docker or [2] Docker Compose:

1. Build by Docker:

   docker build . -t glpi:mytag

2. Build by Docker Compose:

   docker compose up -d   

NOTE! Locate all files from my source, including the Dockerfile and/or Docker Compose YML file in the same directory. Docker commands also are used in that directory.
