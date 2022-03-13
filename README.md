# 1. Create docker network

```
docker network create nginx-proxy
```

<br>

# 2. Run nginx-proxy docker-compose first before run sites

```
docker-compose up --build --force-recreate --no-deps -d
```

<br>

# 3. Then run your website in directory "sites"

- Create directory for example **domain.com**
- Edit **.env** file

PORT List :

```
VIRTUAL_PORT=80 <- For HTML only
VIRTUAL_PORT=3000+ <- For JS
VIRTUAL_PORT=9000 <- For PHP-FPM
```

If Runing **HTML** This Variable is required :

```
DOMAIN=localhost
VIRTUAL_PORT=80
VIRTUAL_HOST=${DOMAIN}

```

If Runing **JS** This Variable is required :

```
PORT=3000 / 3001 / 3002
VIRTUAL_PORT=${PORT}
```

If Runing **PHP** This Variable is required :

```
DOMAIN=php.localhost
VIRTUAL_PORT=9000
VIRTUAL_ROOT=/var/www/public/${DOMAIN}
VIRTUAL_HOST=${DOMAIN}
VIRTUAL_PROTO=fastcgi
```

For SSL Generator add in your .env

```
LETSENCRYPT_HOST=${DOMAIN}
LETSENCRYPT_EMAIL=webmaster@${DOMAIN}
```

<br>

- Edit **/domain.com/docker-compose.yml** file

If you running **HTML** change volumes with this :

```
volumes:
    - ./:/usr/share/nginx/html
```

If you running **JS** change volumes with this :

```
volumes:
    - ./:/app
    - /app/node_modules
```

If you running **PHP** change volumes with this :

```
volumes:
    - ./:/var/www/public/dev.localhost
```

> Ps : change **dev.localhost** with your **VIRTUAL_ROOT** in .env file

<br>

- And run :

```
cd ./sites/domain.com
docker-compose up --build --force-recreate --no-deps -d
```

<br>
<br>

NOTE :
<br>
if you running in Local Development with nginx-proxy VIRTUAL_HOST . Edit your internal files hosts

- Windows : C:\Windows\System32\drivers\etc\hosts
- Linux or Mac : /etc/hosts

```
127.0.0.1 dev.localhost
```