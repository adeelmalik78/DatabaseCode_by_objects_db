# How to Setup a PostgreSQL database in a Docker container

Follow these steps if you are setting up a PostgreSQL database using a docker container:

1. Pull down the docker image from Docker Hub (https://hub.docker.com/_/postgres):
```sh
docker pull postgres
```

2. Start the docker container named "postgres" using "docker run" command:
```sh
docker run \
    --name postgres \
    -p 5432:5432 \
    -e POSTGRES_PASSWORD=secret \
    -d postgres
```

3. Copy the dvdrental.tar to the container using "docker cp" command:
```sh
docker cp ~/Downloads/dvdrental.tar postgres:/
```

4. Get inside the container using "docker exec" command:
```sh
docker exec \
    -it \
    postgres \
    /bin/bash
```

5. Inside the container, run psql to create "dvdrental" database
```sh
psql -U postgres
postgres=# CREATE DATABASE dvdrental;
postgres=# \l
postgres=# \q
```

6. Inside the container, run pg_restore using dvdrental.tar
```sh
pg_restore -U postgres -d dvdrental dvdrental.tar
```

---