---
slug: swappiness
id: nzslxqav3vzn
type: challenge
title: Verify the system roles and configurations were applied.
teaser: Verify the system roles and configurations were applied.
notes:
- type: text
  contents: 'Step 3: Verify the system roles and configurations were applied.'
tabs:
- title: Shell
  type: terminal
  hostname: rhel
- title: client1
  type: terminal
  hostname: client1
- title: client2
  type: terminal
  hostname: client2
difficulty: basic
timelimit: 1
---
Now that the playbook has been applied to the system, verify that the updated settings have been applied. Below you will see we use swappiness, but you could look at any of the included parameters.
```
cat /proc/sys/vm/swappiness
```
The result should be the following.
<pre>
20
</pre>
As expected, the setting is now 20 instead of what it started as in the beginning of the lab.

To verify that session recording is now working, ssh to the system as the rhel user.
```
ssh rhel@localhost
```
Here's the output.
<pre>
# ssh rhel@localhost
The authenticity of host 'localhost (::1)' can't be established.
ED25519 key fingerprint is SHA256:8xzWvasYF07l4QRxYXlX6kr8h4Iqfm/4x+3srCkIdfo.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'localhost' (ED25519) to the list of known hosts.
Locale charset is ANSI_X3.4-1968 (ASCII)
Assuming locale environment is lost and charset is UTF-8

ATTENTION! Your session is being recorded!

[rhel@rhel ~]$
</pre>
To complete this section enter the following.
```
exit
```
You should have seen dialog similar to the output shown above. Success! the system is now recording terminal sessions for users connecting to it.

For `client1` and/or `client2`, repeat the following command.
```
ssh rhel@client1
```
<pre>
root@rhel:~# ssh rhel@client1

ATTENTION! Your session is being recorded!
</pre>
Exit and continue to the next challenge.
```
exit
```