---
title: "Firewalld Rocky Linux"
date: 2021-12-03T10:38:00+04:00
draft: true
---

# Setup Firewalld with Rocky Linux 8 and limit by zone

### Create a new zone :
``` 
firewall-cmd --new-zone=myzone --permanent 
firewall-cmd --reload
firewall-cmd --get-zones
``` 

### Restrict/Allow access

```
firewall-cmd --zone=myzone --add-source=192.168.1.10/32 --permanent
firewall-cmd --zone=myzone --add-port=443/tcp  --permanent
firewall-cmd --reload
```
Or by service:
```
firewall-cmd --zone=myzone --add-source=192.168.1.10/32 --permanent
firewall-cmd --zone=myzone --add-service=https  --permanent
firewall-cmd --reload
```

### List all rules in zone

```
firewall-cmd --zone=myzone --list-all 
```

### Remove source IP
```
firewall-cmd --zone=myzone --remove-source=192.168.1.10/32 --permanent
firewall-cmd --reload
```
### Remove port
```
firewall-cmd --zone=myzone --remove-port=443/tcp --permanent
firewall-cmd --reload
```

### Delete entire zone
```
firewall-cmd --delete-zone=myzone --permanent
firewall-cmd --reload
```