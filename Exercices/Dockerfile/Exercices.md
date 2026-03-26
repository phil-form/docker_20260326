# 1) Dockerfile

Write a dockerfile for an simple http(s) application using nginx. 

Create a index.html in the current folder 
```html
<h1>Hello !!</h1>
```

Copy the content of that html file into the nginx default folder.

Expose the ports 80 and 443.


```Dockerfile
FROM nginx

EXPOSE 80 443

COPY ./webroot /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/nginx.conf

```

```nginx
events {}

http {
    server {
        listen 80;
        server_name localhost;

        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }

    server {
        listen 443 ssl;
        server_name localhost;

        ssl_certificate /etc/nginx/ssl/certificate.crt;
        ssl_certificate_key /etc/nginx/ssl/private.key;

        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}

```

```shell
# Generate self-signed certificates :
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate.crt
# Start the container with the certificates : 
docker run -it -p 80:80 -p 443:443 -v ./ssl:/etc/nginx/ssl/:ro example-nginx
```
