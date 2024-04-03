## Items to change

This items have to be personalized by your need for each service name and deployment mode
For this items naming convention is added with a comment in the compose file.

1. image name
2. container name which is better to be as same as image name
3. port which default is 3306 and exposing pattern would be 3310+
4. network name
5. data volume name
6. username for mariadb
7. database name for mariadb
8. database ur password
9. database rt password (root password)
10. data storing volume name
11. network name

## pre-requisite

1. a network created in docker with the exact name of item 11

```sh
docker network create -d bridge application-net-mode
```

## Build Command

```sh
## 1. for not exposing the passwords or storing in env variables
APPLICATION_SERVICE_MODE_MARIADB_UR_PASSWORD="urpassword" APPLICATION_SERVICE_MODE_MARIADB_RT_PASSWORD="rtpassword" docker compose -f ./docker-compose.mariadb.yml -p application_service_mariadb_mode up -d

## 2. storing as env variables

### step1: making an .env file and storing the passwords here
vim service/.env

### step2: add passwords to the .env file with vim
APPLICATION_SERVICE_MODE_MARIADB_UR_PASSWORD="urpassword"
APPLICATION_SERVICE_MODE_MARIADB_RT_PASSWORD="rtpassword"

### step3: verify passwords are saved
echo $SERVATINO_MARIADB_UR_PASSWORD
echo $SERVATINO_MARIADB_RT_PASSWORD

### step4: docker compose up
docker compose -f ./docker-compose.mariadb.yml -p application_service_mariadb_mode up -d
docker-compose -f ./docker-compose.mariadb.yml -p application_service_mariadb_mode up -d
```

## Testing

```sh
docker exec -it application_service_mariadb_mode /bin/bash
# mariadb -D {DATABASE_NAME -> item 7} -u {DATABASE_USERNAME -> item 6} -p
mariadb -D application_service_db -u application -p

# this will now wants the password and you can enter UR password
# running this select command we will be assured that our database is up and running
SELECT @@character_set_database, @@collation_database;
```
