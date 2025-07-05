**Command to create a volume**

`docker volume create inno-dkr-04-volume`

**Command to list volumes**

`docker volume ls`

**Command to inspect volume**

`docker volume inspect myvolume`

```
docker run -d \
  --name inno-dkr-04 \
  -p 127.0.0.1:8891:80 \
  -v $PWD/nginx.conf:/etc/nginx/nginx.conf \
  -v inno-dkr-04-volume:/var/log/nginx/external \
  nginx:stable
```

**Result video**

[Result video](../Videos/docker3.mkv)