*Docker file*
```
FROM ubuntu:18.04

RUN apt-get update && apt-get install -y\
  nginx

RUN useradd --no-create-home --shell /bin/false nginx

COPY nginx.conf /etc/nginx/nginx.conf

WORKDIR /etc/nginx/

VOLUME ["/var/lib/nginx"]

ENTRYPOINT ["nginx"]

CMD ["-g", "daemon off;"]
```
It is important to add nginx user to the docker file instructions, otherwise the container will not start!

`RUN useradd --no-create-home --shell /bin/false nginx`

*Command to build the image*
`docker build -t nginx:inno-dkr-09 .`

**Result video**

[Result video](../Videos/docker8.mkv)
