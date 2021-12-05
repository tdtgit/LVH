# WIP - LVH (OpenLitespeed - Varnish - Haproxy)
[![Test Docker Compose](https://github.com/tdtgit/LVH/actions/workflows/docker.yml/badge.svg)](https://github.com/tdtgit/LVH/actions/workflows/docker.yml)

## How to use
```docker-compose up -d```
That's it!

## At the first run
```docker-compose exec litespeed /bin/sh /usr/local/lsws/admin/misc/admpass.sh```

## Let's Encrypt SSL certificate request
Run inside LVH directory:
```
docker run -it --rm --name certbot \
    -v "$(pwd)/letsencrypt:/etc/letsencrypt" \
    -v "/root/.cloudflare:/root/.cloudflare" \
    certbot/dns-cloudflare certonly --dns-cloudflare --dns-cloudflare-credentials /root/.cloudflare/cloudflare.ini \
    -d datuan.dev -d *.datuan.dev
```