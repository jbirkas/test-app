# React app subdirectory

## Code changes

- index.html ```<base href="%PUBLIC_URL%/">```
- package.json ```"homepage": "/test/",```

## Nginx configs

- docker/default.conf - container inside config
- nginx/default.conf - frontend nginx proxy

## Local development

Uncomment and edit the ```PUBLIC_URL``` env variable in the ```.env.local``` file for locally changing the URL.

## Build

```bash
npm install
npm run build
docker build -f docker/Dockerfile -t test-app:latest .
```

## Run
```bash
docker network create test-net --gateway=10.10.100.1 --subnet=10.10.100.0/24
docker run -d --restart always --name test-app --network test-net test-app 
docker run -d --restart always --name nginx --network test-net -p 80:80 -v `pwd`/nginx:/etc/nginx/conf.d nginx:mainline-alpine
```


