## Security group
1. Allow HTTP on port 80 for load balancer (rule)
2. Allow HTTP on port  80 from load balancer's IP on proxy machines (rule)

## Instances
1. One instance for load balancer
2. Two instances for proxy/website

## Configs (`/etc/nginx/nginx.conf`) for:
### Load balancer

```
http {
    upstream backend_servers {
        server backend-1-private-ip:80;   # Replace with private IP of backend 1
        server backend-2-private-ip:80;   # Replace with private IP of backend 2
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend_servers;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
}

```

### Proxy

```
http {
    server {
        listen 80;

        location / {
            root /var/www/html;          # Local path to the website files (if hosting static content)
            index index.html index.htm; # Default files to serve
        }

        # Proxy example if forwarding to another backend
        # location / {
        #     proxy_pass http://backend-service-ip:80; 
        #     proxy_set_header Host $host;
        #     proxy_set_header X-Real-IP $remote_addr;
        #     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        # }
    }
}
