After cloning the project you can do this:
Change the .env file DB_HOST: mysql, which must be same name mysql in the docker-compose.yaml file:
  mysql:
    image: mysql:8.0
    container_name: laravel-mysql
    ………
   ……….

You can change both to anything you want , but remember both should be same like DB:HOST:database in env and database in docker-compose.yaml file:
  database:
    image: mysql:8.0
    container_name: laravel-mysql
    ………
   ……….
1.  ( Optional ) If you want to avoid typing sudo whenever you run the docker command, add your username to the docker group:
sudo usermod -aG docker ${USER}
To apply the new group membership, log out of the server and back in, or type the following:
su - ${USER}
You will be prompted to enter your user’s password to continue.

Confirm that your user is now added to the docker group by typing:
groups
Output
sammy sudo docker

If you are comfortable with sudo then just add the sudo  in docker cmd’s like:
sudo docker compose down
sudo docker compose up -d

2. Give permission to this file by running below cmds serially:-
docker exec -it --user root laravel_app bash
chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
chmod -R 775 /var/www/storage /var/www/bootstrap/cache
exit
 and then:-
docker compose down
docker compose up -d

3. If the step 2 does not work then do this(optional):-
docker exec -it --user root laravel_app bash
mkdir -p /var/www/storage/framework/views
mkdir -p /var/www/storage/framework/cache
mkdir -p /var/www/storage/framework/sessions
And then:
chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
chmod -R 775 /var/www/storage /var/www/bootstrap/cache
exit
At last :-
docker compose down
docker compose up -d
Now you can access your 


Some Docker Useful commands:-
sudo systemctl restart docker : to restart the docker
docker compose up --build -d: Builds images before starting containers in detached mode. (for the first time when installing containers only)
docker compose up --build: Builds images before starting containers and attaches the terminal output. (for the first time when installing containers only)
docker compose up -d: Starts containers in detached mode (in the background).
docker compose up: Starts containers and attaches the terminal output.


docker compose restart: restart the containers 
docker compose ps: Lists the status of containers managed by docker compose.
docker compose down: Stops and removes containers, networks, volumes, and images created by up.
docker compose logs [service]: Displays log output from services.
docker compose exec [service] [command]: Executes a command in a running service container. Like:-
 docker exec -it laravel_app bash
php artisan config:cache
php artisan config:clear
php artisan cache:clear
php artisan view:clear 
exit
docker compose build [service]: Builds or rebuilds services.
docker compose restart [service]: Restarts a service.
docker compose stop [service]: Stops a service.




After cloning the project you can do this:
Change the .env file DB_HOST: mysql, which must be same name mysql in the docker-compose.yaml file:
  mysql:
    image: mysql:8.0
    container_name: laravel-mysql
    ………
   ……….

You can change both to anything you want , but remember both should be same like DB:HOST:database in env and database in docker-compose.yaml file:
  database:
    image: mysql:8.0
    container_name: laravel-mysql
    ………
   ……….
1.  ( Optional ) If you want to avoid typing sudo whenever you run the docker command, add your username to the docker group:
sudo usermod -aG docker ${USER}
To apply the new group membership, log out of the server and back in, or type the following:
su - ${USER}
You will be prompted to enter your user’s password to continue.

Confirm that your user is now added to the docker group by typing:
groups
Output
sammy sudo docker

If you are comfortable with sudo then just add the sudo  in docker cmd’s like:
sudo docker compose down
sudo docker compose up -d

2. Give permission to this file by running below cmds serially:-
docker exec -it --user root laravel_app bash
chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
chmod -R 775 /var/www/storage /var/www/bootstrap/cache
exit
 and then:-
docker compose down
docker compose up -d

3. If the step 2 does not work then do this(optional):-
docker exec -it --user root laravel_app bash
mkdir -p /var/www/storage/framework/views
mkdir -p /var/www/storage/framework/cache
mkdir -p /var/www/storage/framework/sessions
And then:
chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
chmod -R 775 /var/www/storage /var/www/bootstrap/cache
exit
At last :-
docker compose down
docker compose up -d
Now you can access your 


Some Docker Useful commands:-
sudo systemctl restart docker : to restart the docker
docker compose up --build -d: Builds images before starting containers in detached mode. (for the first time when installing containers only)
docker compose up --build: Builds images before starting containers and attaches the terminal output. (for the first time when installing containers only)
docker compose up -d: Starts containers in detached mode (in the background).
docker compose up: Starts containers and attaches the terminal output.


docker compose restart: restart the containers 
docker compose ps: Lists the status of containers managed by docker compose.
docker compose down: Stops and removes containers, networks, volumes, and images created by up.
docker compose logs [service]: Displays log output from services.
docker compose exec [service] [command]: Executes a command in a running service container. Like:-
 docker exec -it laravel_app bash
php artisan config:cache
php artisan config:clear
php artisan cache:clear
php artisan view:clear 
exit
docker compose build [service]: Builds or rebuilds services.
docker compose restart [service]: Restarts a service.
docker compose stop [service]: Stops a service.