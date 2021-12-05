# WIP - LVH (OpenLitespeed - Varnish - Haproxy)
[![Test Docker Compose](https://github.com/tdtgit/LVH/actions/workflows/docker.yml/badge.svg)](https://github.com/tdtgit/LVH/actions/workflows/docker.yml)

## How to use
1. Clone LVH source code to your server:
```
$ git clone https://github.com/tdtgit/LVH && cd LVH
```
2. Run the stack:
```
$ docker-compose up -d
```
That's it!

## Stack information
* OpenLitespeed (latest):
  * HTTP & HTTPs for public access: https://server-ip
  * WebAdmin console: https://server-ip:7080
* Varnish (stable - `6.0 LTS`):
  * No public access
  * Access from inside container: `http://varnish`
* Haproxy (latest):
  * Web statistics report: https://server-ip:8080
  * Your backend bind ports...


## At the first run
Setup password for OpenLitespeed WebAdmin Console (http://server-ip:7080):

```docker-compose exec litespeed /bin/sh /usr/local/lsws/admin/misc/admpass.sh```


### Let's Encrypt SSL certificate request
Run inside LVH directory:
```
docker run -it --rm --name certbot \
    -v "$(pwd)/letsencrypt:/etc/letsencrypt" \
    -v "/root/.cloudflare:/root/.cloudflare" \
    certbot/dns-cloudflare certonly --dns-cloudflare --dns-cloudflare-credentials /root/.cloudflare/cloudflare.ini \
    -d datuan.dev -d *.datuan.dev
```
