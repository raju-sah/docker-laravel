# Laravel Docker Setup

After cloning the project, follow these steps to set up your environment:

## Configuration

1. **Update the `.env` file:**
   - Set the `DB_HOST` value to `mysql` (which must match the service name in the `docker-compose.yaml` file).

    ```env
    DB_HOST=mysql
    ```

    ```yaml
    services:
      mysql:
        image: mysql:8.0
        container_name: laravel-mysql
        ...
    ```

    - You can change the name to anything you prefer, but ensure that both the `.env` file and `docker-compose.yaml` file have matching names. For example:

    ```env
    DB_HOST=database
    ```

    ```yaml
    services:
      database:
        image: mysql:8.0
        container_name: laravel-mysql
        ...
    ```

## Docker Commands

2. **Running Docker without sudo (Optional):**
   - Add your username to the docker group to avoid typing `sudo`:

    ```sh
    sudo usermod -aG docker ${USER}
    ```

    - Apply the new group membership by logging out and back in, or type:

    ```sh
    su - ${USER}
    ```

    - Confirm that your user is now added to the docker group:

    ```sh
    groups
    ```

    Output should include `docker`:
    
    ```sh
    sammy sudo docker
    ```

    - If you prefer using sudo, just prepend `sudo` to your docker commands:

    ```sh
    sudo docker compose down
    sudo docker compose up -d
    ```

3. **Setting Permissions:**
   - Give permission to the necessary files by running these commands:

    ```sh
    docker exec -it --user root laravel_app bash
    chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
    chmod -R 775 /var/www/storage /var/www/bootstrap/cache
    exit
    ```

    - Then, restart the containers:

    ```sh
    docker compose down
    docker compose up -d
    ```

4. **Alternative Permissions Setup (Optional):**
   - If the previous step does not work, run these commands:

    ```sh
    docker exec -it --user root laravel_app bash
    mkdir -p /var/www/storage/framework/views
    mkdir -p /var/www/storage/framework/cache
    mkdir -p /var/www/storage/framework/sessions
    chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
    chmod -R 775 /var/www/storage /var/www/bootstrap/cache
    exit
    ```

    - Restart the containers:

    ```sh
    docker compose down
    docker compose up -d
    ```

## Docker Commands

- **Restart Docker:**

    ```sh
    sudo systemctl restart docker
    ```

- **Build and Start Containers:**

    ```sh
    docker compose up --build -d   # First time install, detached mode
    docker compose up --build      # First time install, attached mode
    docker compose up -d           # Detached mode
    docker compose up              # Attached mode
    ```

- **Container Management:**

    ```sh
    docker compose restart         # Restart containers
    docker compose ps              # List status of containers
    docker compose down            # Stop and remove containers, networks, volumes, images
    docker compose logs [service]  # Display log output
    docker compose exec [service] [command] # Execute command in a running service container
    docker compose build [service] # Build or rebuild services
    docker compose restart [service] # Restart a service
    docker compose stop [service]  # Stop a service
    ```

## Laravel Artisan Commands

- **Execute Artisan commands in the container:**

    ```sh
    docker exec -it laravel_app bash
    php artisan config:cache
    php artisan config:clear
    php artisan cache:clear
    php artisan view:clear
    exit
    ```
