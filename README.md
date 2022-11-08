# pleroma-setup

Based on https://docs-develop.pleroma.social/backend/installation/otp_en/

## Create a droplet on Digital Ocean

* Region (close to you)
* Ubuntu 20.04
* Cheapest droplet $4/month (we'll try to upgrade it if needed)
* Setup authentication method (will assume password below)
* Add metrics and alerting (it's free)
* Enable backups (+$0.80)
* Give it a nice name

The ip is in the list of droplets in Digital Ocean

## Set up DNS

In your DNS settings for your domain make an A record

* Name: subdomain that you want to use for this
* Time to live (TTL) : 3600
* Type: A
* Content: IP of your droplet

## Ssh into the droplet

Make a bash variable to hold your IP (replace IP address below)

~~~bash
export IP=<IP ADDRESS>
~~~

~~~bash
ssh root@$IP
~~~

* Say yes to if you want to continue connecting
* Type in the password

## Update the droplet

~~~bash
apt update
apt upgrade -y
~~~

## Install dependencies

~~~bash
apt install -y curl unzip libncurses5 postgresql postgresql-contrib nginx certbot libmagic-dev
~~~

~~~bash
apt install -y imagemagick ffmpeg libimage-exiftool-perl
~~~

~~~bash
apt install -y postgresql-12-rum
~~~

~~~bash
systemctl restart postgresql
~~~

## Install Pleroma

### Create user

~~~bash
adduser --system --shell  /bin/false --home /opt/pleroma pleroma
~~~

### 

~~~bash
export FLAVOUR="amd64"
~~~

~~~bash
su pleroma -s $SHELL -lc "
curl 'https://git.pleroma.social/api/v4/projects/2/jobs/artifacts/stable/download?job=$FLAVOUR' -o /tmp/pleroma.zip
unzip /tmp/pleroma.zip -d /tmp/
"
~~~

~~~bash
su pleroma -s $SHELL -lc "
mv /tmp/release/* /opt/pleroma
rmdir /tmp/release
rm /tmp/pleroma.zip
"
~~~

~~~bash
mkdir -p /var/lib/pleroma/uploads
chown -R pleroma /var/lib/pleroma
~~~

~~~bash
mkdir -p /var/lib/pleroma/static
chown -R pleroma /var/lib/pleroma
~~~

~~~bash
mkdir -p /etc/pleroma
chown -R pleroma /etc/pleroma
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma_ctl instance gen --output /etc/pleroma/config.exs --output-psql /tmp/setup_db.psql"
~~~

Enter:
* domain you used in DNS (example pleroma.patricia.no)
* Give it a name (example Turtle Talk)
* admin email
* notification email
* yes to seach engines and storing in database
* Accept the defaults for hostname, db name, user and password
* yes to RUM indices
* Accept default port and ip
* Accept default dir for media and custom public files
* yes to stripping location from images
* yes to anon names of files
* yes to deduplication

~~~bash
su postgres -s $SHELL -lc "psql -f /tmp/setup_db.psql"
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma_ctl migrate"
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma_ctl migrate --migrations-path priv/repo/optional_migrations/rum_indexing/"
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma daemon"
~~~

~~~bash
sleep 20 && curl http://localhost:4000/api/v1/instance
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma stop"
~~~

Lets do our required reboot here

~~~bash
reboot
~~~

~~~bash
ssh root@$IP
~~~

~~~bash
systemctl stop nginx
~~~

~~~bash
export DOMAIN=<DOMAIN FOR YOUR PLEROMA>
~~~

~~~bash
certbot certonly --standalone --preferred-challenges http -d $DOMAIN
~~~

* admin email address
* Accept terms
* Say no to emails

~~~bash
cp /opt/pleroma/installation/pleroma.nginx /etc/nginx/sites-available/pleroma.conf
ln -s /etc/nginx/sites-available/pleroma.conf /etc/nginx/sites-enabled/pleroma.conf
~~~

We will need to replace all of the `example.tld` in the config file

~~~bash
grep example.tld /etc/nginx/sites-enabled/pleroma.conf
~~~

~~~bash
sed -i "s/example.tld/$DOMAIN/g" /etc/nginx/sites-enabled/pleroma.conf 
~~~

~~~bash
grep $DOMAIN /etc/nginx/sites-enabled/pleroma.conf
~~~

~~~bash
nginx -t
~~~

~~~bash
cp /opt/pleroma/installation/pleroma.service /etc/systemd/system/pleroma.service
~~~

~~~bash
systemctl start pleroma
~~~

~~~bash
systemctl enable pleroma
~~~

~~~bash
mkdir -p /var/lib/letsencrypt
~~~

Uncomment this section

~~~
    # location ~ /\.well-known/acme-challenge {
    #     root /var/lib/letsencrypt/;
    # }
~~~

~~~bash
nano /etc/nginx/sites-enabled/pleroma.conf
~~~

~~~bash
nginx -t
~~~

~~~bash
systemctl restart nginx
~~~

~~~bash
certbot renew --cert-name $DOMAIN --webroot -w /var/lib/letsencrypt/ --dry-run --post-hook 'systemctl reload nginx'
~~~

~~~bash
echo '#!/bin/sh
certbot renew --cert-name example.tld --webroot -w /var/lib/letsencrypt/ --post-hook "systemctl reload nginx"
' > /etc/cron.daily/renew-pleroma-cert
~~~

~~~bash
sed -i "s/example.tld/$DOMAIN/g" /etc/cron.daily/renew-pleroma-cert
~~~

~~~bash
chmod +x /etc/cron.daily/renew-pleroma-cert
~~~

~~~bash
run-parts --test /etc/cron.daily
~~~

~~~bash
cd /opt/pleroma
~~~

~~~bash
export ADMIN_USER=<USER NAME>
export ADMIN_EMAIL=<USER EMAIL ADDRESS>
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma_ctl user new $ADMIN_USER $ADMIN_EMAIL --admin"
~~~

Copy URL, use it to set your password
