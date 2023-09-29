# Docker Proxy Server

## Requirements
- [docker](https://www.docker.com/)

## Installation

1. Clone this repo:
    ```sh
    git clone git@github.com:dedecube/docker-nginx
    ```


2. Create .env file copying .env.example file:
    ```sh
    cp .env.example .env
    ```

3. Create a docker network:
    
    ```sh
    docker network create ${NETWORK_NAME}
    ```
4. Set you NETWORK_NAME into .env file.
   
5. Build docker-compose:
   
   ```sh
    docker compose build
   ```

6. Run docker container:

    ```sh
    docker compose up
    ```

    > Optionally, you can add `-d` flag to run it detached.

## Graph

```mermaid
stateDiagram-v2
    DigitalOcean --> Vps: firewall

    state Vps {
        Docker
        Native
    }

    state Native {
        MySQL
    }

    state Docker {
        ProxyServer
        ProxyServer --> LaravelProject1
        ProxyServer --> LaravelProject2
        ProxyServer --> LaravelProjectN

        state LaravelProject1 {
            Laravel_Project_1_Nginx : nginx
            Laravel_Project_1_Php_Fpm : php-fpm
        }

        state LaravelProject2 {
            Laravel_Project_2_Nginx : nginx
            Laravel_Project_2_Php_Fpm : php-fpm

        }

        state LaravelProjectN {
            Laravel_Project_N_Nginx : nginx
            Laravel_Project_N_Php_Fpm : php-fpm

        }
    }

    LaravelProject1 --> MySQL
    LaravelProject2 --> MySQL
    LaravelProjectN --> MySQL

```