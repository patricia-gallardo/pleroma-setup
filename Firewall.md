# Configure Firewall : ufw (Uncomplicated Firewall)

**WARNING: MAKE SURE TO ALLOW SSH**

## Check status

Expected output `Status: inactive`

~~~bash
ufw status
~~~

## Allow ssh

~~~bash
ufw allow ssh
~~~

## Allow http

~~~bash
ufw allow http
~~~

## Allow https

~~~bash
ufw allow https
~~~

## Enable firewall

~~~bash
ufw enable
~~~

## Check status

~~~bash
ufw status verbose
~~~

Example output

~~~
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
443/tcp                    ALLOW IN    Anywhere                  
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443/tcp (v6)               ALLOW IN    Anywhere (v6)
~~~

## Reboot

~~~bash
reboot
~~~
