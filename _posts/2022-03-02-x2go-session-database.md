---
layout: post
---

A couple of us at Kratos were running into an issues where our x2go sessions were not suspending correctly.

After looking into the x2gosuspend-session script, I found that this command is failing:

```
/usr/lib64/x2go/x2gogetagent $X2GO_SESSION
```

It looks like /var/lib/x2go/x2go\_sessions is getting corrupted somehow.

One quick way to regen that file:
```
systemctl disable x2gocleansessions.service
rm -f /var/lib/x2go/x2go_sessions
/usr/sbin/x2godbadmin --createdb
systemctl enable x2gocleansessions.service
```
