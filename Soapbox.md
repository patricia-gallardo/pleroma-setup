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

### Set default post privacy

1. __Public__ posts can be sent all over the fediverse and end up in their fedirated timelines. **This is most likely NOT what you want.**
1. __Ulisted__ goes to your followers and are visible on the webpage
1. __Followers-only__ goes only to followers, and not on the webpage

Instructions

* Go to settings : https://$DOMAIN/settings
* Set `Default post privacy` to `Unlisted
* It should save automatically
* Reload the page
* Test by clicking the `Compose` button and check that there isn't a globe there
