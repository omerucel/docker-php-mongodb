# About

PHP project skeleton with docker. 

# Build

```bash
$ docker build -t ou/php-nginx-mongo .
```

# Run

```bash
$ cp docker-compose.yml.sample docker-compose.yml
$ docker-compose up -d
```

# How can i access to the container?

Run following command to find container ID:

```bash
$ docker ps
```

Then run following command with container ID:

```bash
$ docker exec -it ContainerID /bin/bash
```

And update composer for your project:

```bash
# cd /data/project
# composer update
```
