# Docker-redis

Dockerized redis-server with cluster enabled, based on docker offical redis image [https://github.com/docker-library/redis]

## Run example

```bash
$ docker run --name redis1 -d jwdaniel/redis
$ docker run --name redis2 -d jwdaniel/redis
$ docker run --name redis3 -d jwdaniel/redis

$ docker run -it --link redis1:redis --rm jwdaniel/redis sh -c 'exec redis-cli -h "$REDIS_PORT_6379_TCP_ADDR" -p "$REDIS_PORT_6379_TCP_PORT"'

$ REDIS1_IPADDR=`docker inspect --format '{{ .NetworkSettings.IPAddress }}' redis1`
$ REDIS2_IPADDR=`docker inspect --format '{{ .NetworkSettings.IPAddress }}' redis2`
$ REDIS3_IPADDR=`docker inspect --format '{{ .NetworkSettings.IPAddress }}' redis3`
$ redis-trib.rb create --replicas 0 $REDIS1_IPADDR:6379 $REDIS2_IPADDR:6379 $REDIS3_IPADDR:6379

```

