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

* Go to the admin panel : https://$DOMAIN/soapbox/admin
* Set Registrations as closed
