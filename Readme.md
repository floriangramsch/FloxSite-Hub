```shell
docker network inspect FloxNet >/dev/null 2>&1 || docker network create FloxNet
```

```
shell docker compose -f blog/docker-compose.yml up -d
```

```
shell docker compose -f api/docker-compose.yml up -d
```

```
shell docker compose -f nginx/docker-compose.yml up -d
```
