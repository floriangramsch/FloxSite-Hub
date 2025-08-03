```shell
docker network inspect FloxNet >/dev/null 2>&1 || docker network create FloxNet
```

```
shell docker compose -f pages/HV-Bingerschlag/docker-compose.yml up -d
```

## Local Network Pages
```bash
mkdir -p services/traefik/certs
cd services/traefik/certs
openssl req -x509 -newkey rsa:2048 -nodes \
  -keyout traefik/certs/<yourpage>.key \
  -out traefik/certs/<yourpage>.crt \
  -days 365 \
  -subj "/CN=<yourpage>.debiansatellite.lan"
```

```bash
# services/traefik/traefik.yml
tls:
  certificates:
    - certFile: /etc/traefik/certs/<yourpage>.crt
      keyFile: /etc/traefik/certs/<yourpage>.key
```

```bash
# pages/<yourpage>/docker-compose.yml
labels:
- "traefik.enable=true"
- "traefik.http.routers.<yourpage>.rule=Host(`<yourpage>.debiansatellite.lan`)"
- "traefik.http.routers.<yourpage>.entrypoints=websecure"
- "traefik.http.routers.<yourpage>.tls=true"
- "traefik.http.services.<yourpage>.loadbalancer.server.port=<port>"
```
