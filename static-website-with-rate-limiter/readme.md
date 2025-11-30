# Nginx Rate Limit config

### How to Start the Project

Start the project

```bash
docker compose up -d
```

This will start a `nginx` container running at port `80` with a virtualHost set in `static.localhost.conf`.


To test the setup, you can open this link in your browser
Go to: 

```bash
http://localhost
```

<!-- Or you can use `curl`

```bash
# for i in {1..10}; do curl -s http://localhost | grep -i "website"; done | wc -l

for i in {1..10}; do curl -s -o /dev/null -w "%{http_code}\n" http://localhost; done

``` -->

Check HTTP status codes 
```bash
for i in {1..10}; do curl -s -o /dev/null -w "%{http_code}\n" http://localhost; done
```

This commands:

Send 10 quick requests to `http://localhost`

- Filter responses containing the word website
- Print how many matches were returned
- Show how many requests returned 200 or 429, depending on the rate-limit behavior

