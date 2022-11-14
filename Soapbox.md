# Soapbox UI for Pleroma

Based on : https://docs.soapbox.pub/frontend/installing/

See also : https://docs-develop.pleroma.social/backend/administration/CLI_tasks/frontend/

~~~bash
export IP=<IP ADDRESS>
~~~

~~~bash
ssh root@$IP
~~~

~~~bash
curl -L https://gitlab.com/soapbox-pub/soapbox/-/jobs/artifacts/develop/download?job=build-production -o soapbox.zip
~~~

~~~bash
busybox unzip soapbox.zip -o -d /var/lib/pleroma
~~~

Reload your instance web page

## Tweak settings

### Close registrations

* Go to the soapbox admin panel (More > Dashboard) : https://$DOMAIN/soapbox/admin
* Set Registrations as closed

### For single user

* Go to the Soapbox config (link in the upper right corner) : https://$DOMAIN/soapbox/config
* Turn on `Single user mode`
* Put in users @
* Scroll down and click save

### Update logo

* Go to the Soapbox config (link in the upper right corner) : https://$DOMAIN/soapbox/config
* Upload logo
* Scroll down and click save
