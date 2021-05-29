## 順番

```
$ mkdir -p app
$ docker volume create fullexample-sync
$ docker volume create simpleexample-sync
$ docker-sync start --foreground

# 別シェル A
$ touch app/somefile.txt
$ COMPOSE_FILE=docker-compose.yml:docker-compose-dev.yml docker-compose up

# 別シェル B
$ echo 'hello' >> app/somefile.txt
$ echo 'hello' >> app/somefile.txt
$ echo 'hello' >> app/somefile.txt
```


## 片付け

```
$ COMPOSE_FILE=docker-compose.yml:docker-compose-dev.yml docker-compose down
$ docker-sync clean
```
