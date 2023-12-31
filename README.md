GLPI server in Docker.

There are 3 docker containers used to launch this GLPI server version:
* GLPI itself (NGINX, PHP v8.2, application files);
* MariaDB server;
* Adminer (database graphical control panel).

It is possible to run all containers [1] separately or [2] by using Docker Compose. See instruction below.

1. Separately:
   docker run -name glpi -d -p 80:80 -p 443:443 alyonamoskalets/glpi:v1
   docker run -name glpi_db -d -p 3306:3306 -e MARIADB_USER=inventory_user -e MARIADB_PASSWORD=pass4DB -e MARIADB_DATABASE=inventory -e MARIADB_ROOT_PASSWORD=pass4Admin -e MARIADB_PORT_NUMBER=3306 -v /glpi/db:/var/lib/mysql mariadb
   docker run -name glpi_cp -d -p 8080:8080 --links glpi_db adminer
2. Using Docker Compose:
   docker compose up -d -f docker-compose-public.yml
