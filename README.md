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
export IP=174.138.2.114
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

~~~bash

~~~

~~~bash

~~~
