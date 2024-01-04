### Getting certs example

1. Up webserver container
    ```bash
    docker compose up -d
    ```
2. Update host into [nginx.conf](nginx/conf/nginx.conf)
    ```nginx configuration pro
    server {
        listen 80;
        listen [::]:80;
    
        server_name example.com www.example.com;
        server_tokens off;
    
        location /.well-known/acme-challenge/ {
            root /var/www/certbot;
        }
    
        location / {
            return 301 https://example.com$request_uri;
        }
    }
    ```

3. Run certbot container and check result with --dry-run option
    ```bash
    docker compose run --rm --dry-run certbot certonly --webroot --webroot-path /var/www/certbot/ --non-interactive --agree-tos --email your_email@example.com -d example.com
    ```

4. Run certbot container and getting certs
    ```bash
    docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ --non-interactive --agree-tos --email your_email@example.com -d example.com
    ```

5. To renew certs
   ```bash
   docker-compose run --rm certbot renew
   ```
