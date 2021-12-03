---
title: "Install and Configure Fail2ban Rocky Linux"
date: 2021-12-03T13:23:23+04:00
draft: false
---

# Install and configure Fail2ban on Rocky Linux 8

> ***Run all commands bellow as root*** 

### Firewall

Enable and start firewalld:

``` systemctl enable firewalld && service firewalld start ```

### Install Fail2ban

``` 
dnf install -y epel-release 
dnf install -y fail2ban fail2ban-firewalld
``` 

Start and enable:

```
systemctl start fail2ban
systemctl enable fail2ban
```
Check if fail2ban is running:
```
systemctl status fail2ban
```

### Configure ssh jail

```
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
mv /etc/fail2ban/jail.d/00-firewalld.conf /etc/fail2ban/jail.d/00-firewalld.local
```

edit configuration for sshd

```
vi /etc/fail2ban/jail.d/sshd.local
```

put the following in it:

```
[sshd]
enabled = true
bantime = 1d
maxretry = 3
```

Restart and enable the jail:
``` 
systemctl restart fail2ban 
```
Check if the jail is working:
``` 
fail2ban-client status sshd 
``` 
It will output something like this:
```
Status for the jail: sshd
|- Filter
|  |- Currently failed:	1
|  |- Total failed:	20
|  `- Journal matches:	_SYSTEMD_UNIT=sshd.service + _COMM=sshd
`- Actions
   |- Currently banned:	2
   |- Total banned:	2
   `- Banned IP list:	49.88.112.73 120.133.56.246
```

### Unban an IP

If you need to unban an IP for any reason:
```
fail2ban-client unban THE_IP_TO_UNBAN
```

