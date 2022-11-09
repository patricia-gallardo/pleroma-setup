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
ufw allow OpenSSH
~~~

## Allow http

~~~bash
ufw allow http
ufw allow "Nginx HTTP"
~~~

## Allow https

~~~bash
ufw allow https
ufw allow "Nginx HTTPS"
~~~

## Allow Nginx

~~~bash
ufw allow "Nginx Full"
~~~

## Allow SMTP

~~~bash
ufw allow 25/udp
~~~

## Enable firewall

~~~bash
ufw enable
~~~

## Check status

~~~bash
ufw status
~~~

Example output

~~~
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere                  
OpenSSH                    ALLOW       Anywhere                  
80/tcp                     ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
443/tcp                    ALLOW       Anywhere                  
Nginx HTTPS                ALLOW       Anywhere                  
Nginx Full                 ALLOW       Anywhere                  
25/udp                     ALLOW       Anywhere                  
22/tcp (v6)                ALLOW       Anywhere (v6)             
OpenSSH (v6)               ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)             
443/tcp (v6)               ALLOW       Anywhere (v6)             
Nginx HTTPS (v6)           ALLOW       Anywhere (v6)             
Nginx Full (v6)            ALLOW       Anywhere (v6)             
25/udp (v6)                ALLOW       Anywhere (v6)  
~~~

## Reboot

~~~bash
reboot
~~~
