# Static Website with Traefik Load Balancer

![alt text](image.png)

<!-- ## Project Overview -->
## Feature

This project demonstrates how to host a website accross multiple containers/servers and balance traffic between them using **[Traefik](https://doc.traefik.io/traefik/)**, a modern HTTP reverse proxy and load balancer.

It is ideal for beginners who want to understand how load balancing works in a **Dockerized environment**.

NB: In this project, `website1` and `website2` are the same, but just for visualisation purpose, I changed a small part of the source code to help user to easily identify which container serve the version of the website displayed in the browser.

### How to Run

1. Clone the repository

```bash
# Clone the repository
git clone https://github.com/tchedem/nginx-playground.git 

# Navigate to the specific example
cd static-website-with-traefik-load-balancer

# Start the services
docker compose -f docker-compose.yml up -d

# This launches all defined services in detached mode:
# Traefik (acting as a reverse proxy / load balancer)
# Website 1 (static Nginx container)
# Website 2 (static Nginx container)
```

### How to test

1. Test in your browser

Go to: 

```bash
http://localhost
```
Make sure to refresh multiple times the page. You should see alternating responses like “My Website 1” and “My Website 2.”
That’s Traefik distributing incoming requests evenly between both Nginx containers (a round-robin load balancing behavior).


2. Test with `curl`
```bash
for i in {1..10}; do curl -s http://localhost | grep -i "website 1"; done | wc -l
```

This runs 10 requests to http://localhost, filters for lines containing “website 1”, and prints matches.

If you repeat the command changing "website 1" to "website 2", you’ll notice both sites respond roughly 50% of the time - confirming Traefik is load balancing correctly.

**Bonus**

```bash
# 2 interresting commands from gen-ai tools (using grep and awk as output filter method)
for i in {1..10}; do curl -s http://localhost; done | grep -o "Website [12]" | sort | uniq -c

for i in {1..10}; do curl -s http://localhost; done | awk '/Website 1/ {w1++} /Website 2/ {w2++} END {print "Website 1:", w1; print "Website 2:", w2}'

```
