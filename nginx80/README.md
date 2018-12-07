# NGINX Dockerfile

`cd nginx80`

`sudo docker build -f Dockerfile -t nginx80-certbot .`

Start the non secure site:
`sudo docker run -p 80:80 -v ~/var/www/letsencrypt:/var/www/letsencrypt -v ~/letsencrypt:/etc/letsencrypt -d nginx80-certbot`

Staging test: **Success!!**
`sudo docker run -it --rm -v ~/var/www/letsencrypt:/var/www/letsencrypt -v ~/letsencrypt:/etc/letsencrypt nginx80:certbot certbot certonly --webroot --agree-tos --no-eff-email --email chris.quan@abracontrols.com -w /var/www/letsencrypt --staging -d demo.meshington.com`

If staging is successful then onto production certs:
`sudo docker run -it --rm -v ~/var/www/letsencrypt:/var/www/letsencrypt -v ~/letsencrypt:/etc/letsencrypt nginx80:certbot certbot certonly --webroot --agree-tos --no-eff-email --email chris.quan@abracontrols.com -w /var/www/letsencrypt -d demo.meshington.com`

Give permission access to certificates:

`cd`
`sudo chmod -R 777 letsencrypt/live/demo.meshington.com`
