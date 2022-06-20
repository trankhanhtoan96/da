# Install

```shell
yum -y install net-tools network-scripts wget perl epel-release
wget https://raw.githubusercontent.com/trankhanhtoan96/da/master/setup.sh
chmod +x setup.sh
sh setup.sh
```

# Setup network

```shell
vi /etc/sysconfig/network-scripts/ifcfg-eth0:100
```

## Content

```shell
DEVICE=eth0:100
IPADDR=176.99.3.34
NETMASK=255.255.255.0
```

# Change network

```shell
/usr/bin/perl -pi -e 's/^ethernet_dev=.*/ethernet_dev=eth0:100/' /usr/local/directadmin/conf/directadmin.conf
ifup eth0:100
```

# Get license

```shell
vi /usr/local/directadmin/scripts/update-license.sh
```

## Content

```shell
#/bin/bash
/usr/sbin/ifdown eth0:100
rm -f /tmp/license.key
rm -f /usr/local/directadmin/conf/license.key
/usr/bin/wget -O /tmp/license.key.gz https://github.com/trankhanhtoan96/da/raw/master/license.key.gz
/usr/bin/gunzip /tmp/license.key.gz
mv /tmp/license.key /usr/local/directadmin/conf/
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
/usr/sbin/ifup eth0:100
/bin/systemctl restart directadmin.service
```

## Excute get license

```shell
sh /usr/local/directadmin/scripts/update-license.sh
```

## Set crontab

```shell
0 12 */3 * * /usr/local/directadmin/scripts/update-license.sh
```

# Use login information

```shell
cat /usr/local/directadmin/scripts/setup.txt
```
