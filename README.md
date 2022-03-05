# 1. Create docker network

```
docker network create nginx-proxy
```

# 2. Run this docker-compose first before run web

```
docker-compose up --build --force-recreate --no-deps -d
```

# 3. Run web in directory

```
cd /www/web.com
docker-compose up --build --force-recreate --no-deps -d
```
