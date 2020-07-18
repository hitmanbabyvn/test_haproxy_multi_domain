# New certificate
sudo certbot certonly --standalone -d demo.scalinglaravel.com \
    --non-interactive --agree-tos --email admin@example.com \
    --http-01-port=8888

# Create cert directory
sudo mkdir -p /etc/ssl/demo.scalinglaravel.com

# HAProxy needs an ssl-certificate to be one file
sudo cat /etc/letsencrypt/live/demo.scalinglaravel.com/fullchain.pem \
    /etc/letsencrypt/live/demo.scalinglaravel.com/privkey.pem \
    | sudo tee /etc/ssl/demo.scalinglaravel.com/demo.scalinglaravel.com.pem

# Renew certificate
sudo certbot renew --tls-sni-01-port=8888

# Automating renewal
0 0 1 * * root bash /opt/update-certs.sh

# Enforcing HTTPS

