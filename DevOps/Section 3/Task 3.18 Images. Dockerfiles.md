**Docker file**

```
FROM nginx:stable
COPY nginx.conf /etc/nginx/nginx.conf
```
**Commands to build and run the images**

docker build -t inno-dkr-08 .

docker run -d \
  -p 127.0.0.1:8900:80 \
  inno-dkr-08

**Result video**

[Result video](../Videos/docker7.mkv)
