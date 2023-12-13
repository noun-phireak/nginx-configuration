# Ningx Configuration http & https

## Nginx Configuration http `web-server.conf`

server {
	listen 80;
	server_name my.domain.tech ;

        location / {
            proxy_set_header  Host $host;
            proxy_pass http://localhost:8000;
    }
}

## Nginx Configuration https `web-server.conf`

server {
       listen         80;
       server_name    my.domain.tech;
       return         301 https://$server_name$request_uri;
}

server {
    listen         443 ssl;
    server_name    my.domain.tech;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_certificate      /etc/ssl/certs/my.domain.tech.pem;
    ssl_certificate_key  /etc/ssl/keys/my.domain.tech.key;

    location / {
        proxy_set_header  Host $host;
        proxy_pass http://localhost:8000;
    }

	  access_log /var/log/nginx/my_domain_access.log;
    error_log /var/log/nginx/my_domain_error.log;
}
