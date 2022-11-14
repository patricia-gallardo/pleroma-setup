# Domain Block List with Message Rewrite Facility (MRF)

Based on : https://plume.bdx.town/~/FaitsDiversE/How%20to%20block%20domains%20in%20Pleroma/
See also docs: https://docs.pleroma.social/backend/configuration/mrf/#using-simplepolicy

* UI : `https://<DOMAIN>/pleroma/admin/#/settings/mrf`
* In `Policies` add `SimplePolicy`
* In `Reject` add all domains to block
* Note: If you add a domain a second time it removes it, so check carefully when adding, it should be added at the end
* Press submit button

## Suggestions

### Public blocklists

* [mastodon.social](https://mastodon.social/about#unavailable-content)
* [weirderearth](https://raw.githubusercontent.com/weirderearth/weirder-rules/main/suggested-instance-blocks.md)
* [hachyderm.io](https://raw.githubusercontent.com/hachyderm/hack/main/blocklist)
* [FediBlock](https://joinfediverse.wiki/FediBlock)

### API blocklists

* [mastodon.social](https://mastodon.social/api/v1/instance/domain_blocks)

### Hate Speech

~~~
bae.st
beefyboys.win
cachapa.moe
chickenfan.club
chudbuds.lol
crlf.ninja
detroitriotcity.com
eientei.org
eveningzoo.club
freecumextremist.com
freesoftwareextremist.com
freespeechextremist.com
gameliberty.club
gearlandia.haus
qoto.org
hunk.city
leafposter.club
masochi.st
mugicha.club
nicecrew.digital
poa.st
rdrama.cc
ryona.agency
seal.cafe
shitpost.cloud
shortstackran.ch
sleepy.cafe
sneed.social
strelizia.net
troll.cafe
varishangout.net
yggdrasil.social
~~~

### Harassment

~~~
bitcoinhackers.org
gab.ai
gab.com
iddqd.social
kiwifarms.cc
kiwifarms.is
kiwifarms.net
noagendasocial.com
shitposter.club
truthsocial.com
truthsocial.co.in
~~~

### Transphobia

~~~
gleasonator.com
spinster.xyz
~~~

## Restart Pleroma

~~~bash
systemctl restart pleroma
~~~
