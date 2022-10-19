

# Name Setting up DNS 

#ssh file to execute process 
`you Can modifiy this file according to your configuration and run.`

# [DNS.sh](http://10.10.9.1:9180/gitlab-instance-ebd9c594/random_code/-/blob/main/src/dns.sh) 
    
### steps 
### Host file 
add below to host file `/etc/hosts`
```bash
10.10.20.111	rac1.racdomain.com	rac1 #DNS
10.10.20.112	rac2.racdomain.com	rac2 #DNS
10.10.30.111	rac1-priv.racdomain.com	rac1-priv
10.10.30.112	rac2-priv.racdomain.com	rac2-priv 
10.10.20.113	rac1-vip.racdomain.com	rac1-vip #DNS
10.10.20.114	rac2-vip.racdomain.com	rac2-vip #DNS
#10.10.20.115	rac-cluster-scan.racdomain.com	rac-cluster-scan #DNS
#10.10.20.116	rac-cluster-scan.racdomain.com	rac-cluster-scan #DNS
#10.10.20.117	rac-cluster-scan.racdomain.com	rac-cluster-scan #DNS

```


## Setup DNS
On first node you can configure DNS but the best practice to have DNS server out of RAC nodes:

### Install BIND9

```bash

# DNS Server
dnf makecache

dnf install bind bind-utils -y

hostnamectl
```

### Configure BIND
```bash
Run dns.sh
```

### Test DNS Configuration
```bash
# check the configurations 
named-checkconf
named-checkzone racdomain.com /var/named/forward.racdomain.com
named-checkzone 10.10.20.111 /var/named/backward.racdomain.com
systemctl start named
systemctl enable named
```

### Use DNS 

```bash

################################
######  DNS Client Node 1 ######
################################

# edit resolv.conf
cat > /etc/resolv.conf <<EOF
search racdomain.com
nameserver 10.10.20.111
EOF

# edit the network profiles may different in your system
nano /etc/sysconfig/network-scripts/ifcfg-enp0s3
# add this line to this file 
DNS1=10.10.20.111

#  allow the dns traffic 

firewall-cmd  --add-service=dns --zone=public  --permanent
firewall-cmd --reload

# test from the client
nslookup rac1
nslookup rac2 

ping rac1
ping rac2
