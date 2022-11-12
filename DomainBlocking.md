# Domain Block List with Message Rewrite Facility (MRF)

Based on : https://plume.bdx.town/~/FaitsDiversE/How%20to%20block%20domains%20in%20Pleroma/

* UI : `https://<DOMAIN>/pleroma/admin/#/settings/mrf`
* In `Policies` add `SimplePolicy`
* In `Reject` add all domains to block
* Press submit button

Restart Pleroma

~~~bash
systemctl restart pleroma
~~~
