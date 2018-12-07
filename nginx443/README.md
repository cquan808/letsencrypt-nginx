# NGINX Dockerfile

`cd`

`cd nginx443`

`docker build -f Dockerfile.nginx443 -t nginx443-certbot .`

`docker run -p 80:80 -p 443:443 -v ~/var/www/letsencrypt:/var/www/letsencrypt -v ~/letsencrypt:/etc/letsencrypt -d nginx443-certbot`

Check at: http://chrisquan.com, redirects to `https`
