## Security group
1. Allow HTTP on port 80 for load balancer (rule)
2. Allow HTTP on port  80 from load balancer's IP on proxy machines (rule)

## Instances
1. One instance for load balancer
2. Two instances for proxy/website

## Configs (`/etc/nginx/nginx.conf`) for:
### Load balancer 
1. Delete default config (if running on Debian based distros) in `/etc/nginx/sites-enabled/default`
2. Delete default config (if running on Debian based distros) in `/etc/nginx/sites-available/default`
3. Create a new files in `/etc/nginx/conf.d/load-balancer.conf`

```
upstream backend {
	least_conn;
	server 3.121.220.132; # ip addres of a blue node
	server 3.75.97.151; # ip addres of a yellow node
	# server ; # ip addres of the backup server
}

server {
	location / {
	  proxy_pass http://backend;
	  proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	}

	access_log /var/log/nginx/load-balancer-access.log;
	error_log /var/log/nginx/load-balancer-error.log;
}
```
2. check nginx config `sudo nginx -t`
3. restart nginx `sudo systemctl restart nginx.service`
### Proxy (nodes)
1.  Delete default config (if running on Debian based distros) in `/etc/nginx/sites-enabled/default`
2. Delete default config (if running on Debian based distros) in `/etc/nginx/sites-available/default`
2. Create config file at /etc/nginx/sites-available/example.com
```
server {
    listen 80;

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

### Video of the result

[Result video](../Videos/2025-01-12 19-13-07.mkv)


!!! check this articles! 
https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/How-to-setup-an-Nginx-load-balancer-examples

https://upcloud.com/resources/tutorials/configure-load-balancing-nginx

https://www.youtube.com/watch?v=ZdMG-vZ5Sjg
