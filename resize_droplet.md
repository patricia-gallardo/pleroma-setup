# Resize droplet

If the droplet is too small we can try to resize it in Digital Ocean

## Shut down droplet

~~~bash
poweroff
~~~

## Take a snapshot

* Click on the droplet and in the left hand panel chose `Snapshots`
* Click on `Take snapshot`

## Resize droplet

1. Press the dots next to the droplet and choose `Resize droplet`
2. We'll try CPU and RAM only
3. Chose the size you want, but have at least 1GB of RAM
4. Click `Resize`

## Start up the droplet

* Click on the droplet and in the left hand panel chose `Power`
* Click on `Turn on`

## Once it is up and looking good

Consider deleting your snapshot since it costs money.
