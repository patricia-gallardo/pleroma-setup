# Users

## Create regular user

~~~bash
export USER_HANDLE=<USER HANDLE>
export USER_EMAIL=<USER EMAIL>
~~~

~~~bash
su pleroma -s $SHELL -lc "./bin/pleroma_ctl user new $USER_HANDLE $USER_EMAIL"
~~~

Copy url at the end of the output and give it to the user
