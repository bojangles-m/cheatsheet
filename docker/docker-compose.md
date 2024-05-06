All instances and their configuration in must be in docker-compose.yml file

## running the following command in the same directory as the file:

```shell
docker compose up
```

## put the service in background

```shell
docker compose up -d
```

## build the containers

```shell
docker compose up --build -d
```

## stop container

```shell
docker compose down
```

## Get log info from containers

```shell
docker compose logs clarify -f
```

## Remove Orphans

```shell
docker compose down --remove-orphans
```
