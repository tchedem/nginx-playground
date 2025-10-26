## Static Website with Docker & Nginx

This directory contans everythings you need to build and run a static website using Docker and Nginx.

### Feature 

Uses Nginx as Webserver/Reverse Proxy to serve static content.

Supports local volume mounting for fast development: changes in `./website` directory || `static.localhost.conf` are reflected immediately in the container.

Designed to be lightweight and easy to extend.

Configurable via Docker Compose.

### How to Run

***Pre-requisites***
You need to have **Docker** installed. Here is the [official guide](https://docs.docker.com/get-started/get-docker/).

```bash
 # Start the containers in detached mode
 docker compose up -d # builds (if needed) and starts the containers in the background.

 # Stop the containers and remove local images & volumes
 docker compose down --rmi local -v # stops the containers and removes associated volumes and locally built images.

 # To test the deployed website 
 for i in {1..100}; do curl http://127.0.0.1:8000/; done;
```

Or, once running, access to your website on the following address: `http://localhost:8000`.


### Structure

- `website` : Contain the static website content (HTML, CSS, JS files)
- `docker-compose.yml` : A Docker Compose yaml file to run the containerized website. While not strictly necessary for asingle Nginx container, I decided to include it for convenience to manage ports, volumes, and service configuration easily.
- `static.localhost.conf` : a standard Nginx Virtual host configuration file that routes the incoming requests to the correct directory of our static website. - *If you are not used to Nginx, I recommend you to try it out on a new installed Virtual Machine.* 


---

2025_10_09