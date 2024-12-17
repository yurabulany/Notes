## Security group
1. Allow HTTP on port 80 for load balancer (rule)
2. Allow HTTP on port  80 from load balancer's IP on proxy machines (rule)

## Instances
1. One instance for load balancer
2. Two instances for proxy/website

## Configs (`/etc/nginx/nginx.conf`) for:
### Load balancer 
1. Create a new file in `/etc/nginx/conf.d/load-balancer.conf`

```
upstream backend_servers {
    server 192.168.1.10:80 max_fails=3 fail_timeout=30s; # ip addres of a node
    server 192.168.1.11:80 max_fails=3 fail_timeout=30s; # ip addres of a node
}

server {
    listen 80;

    location / {
        proxy_pass http://backend_servers;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
}


```
2. check nginx config `sudo nginx -t`
3. restart nginx `sudo systemctl restart nginx.service`
### Proxy
1. Create config file at /etc/nginx/sites-available/example.com
```
server {
    listen 80;
    server_name 3.71.50.224; #ip address of the ec2 instance

    root /var/www/html;
    index blue.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
2. Create symbolic link for  /etc/nginx/sites-available/example.com to /etc/nginx/sites-enabled/ `ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/`
3.  check nginx config `sudo nginx -t`
4. restart nginx `sudo systemctl restart nginx.service`


!!! check this article! 
https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/How-to-setup-an-Nginx-load-balancer-examples