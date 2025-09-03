# Docker

#### Docker Restart

The `docker restart always` policy automatically restarts a container whenever it stops, regardless of the exit status. It is useful for ensuring the high availability of critical services, like a web server or database.&#x20;

Using Docker Compose

In a `docker-compose.yml` file, set the restart policy under a service: yaml

```
version: '3'
services:
  my-service:
    image: my-image
    restart: always
```
