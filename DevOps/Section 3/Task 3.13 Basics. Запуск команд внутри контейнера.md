Run the container

```
docker run -d \
        --name inno-dkr-03 \
        -p 127.0.0.1:8890:80 \
        -v /home/yura/Yura/projects/learn_devops/nginx.conf:/etc/nginx/nginx.conf \
        nginx:stable
```

Command to run inside the container (reloads nginx) `docker exec inno-dkr-03 nginx -s reload`

When changing a host file with Vim **may not work** on the container!

[Result video](../Videos/docker2.mkv)
