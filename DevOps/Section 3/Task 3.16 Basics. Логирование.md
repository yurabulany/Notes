```
 docker run -d \
  --name inno-dkr-06-local \
  -p 127.0.0.1:8892:80 \
  -v $PWD/nginx.conf:/etc/nginx/nginx.conf \
  --log-driver local --log-opt max-size=10m \
  nginx:stable


docker run -d \
  --name inno-dkr-06-global \
  -p 127.0.0.1:8893:80 \
  -v $PWD/nginx.conf:/etc/nginx/nginx.conf \
  nginx:stable
```

**Result video**

[Result video](../Videos/docker5.mkv)
```
```
