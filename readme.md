```shell
yum -y install net-tools network-scripts wget perl epel-release
```

```shell
vi /etc/sysconfig/network-scripts/ifcfg-eth0:100
```
```shell
DEVICE=eth0:100
IPADDR=176.99.3.34
NETMASK=255.255.255.0
```

```shell
/usr/bin/perl -pi -e 's/^ethernet_dev=.*/ethernet_dev=eth0:100/' /usr/local/directadmin/conf/directadmin.conf
ifup eth0:100
```

```shell
vi /usr/local/directadmin/scripts/update-license.sh
```
```shell
#/bin/bash
# --- Điền lại tên subinterface gia hạng license nhé! --- #
/usr/sbin/ifdown eth0:100
rm -f /tmp/license.key
rm -f /usr/local/directadmin/conf/license.key
/usr/bin/wget -O /tmp/license.key.gz https://github.com/damvt/directadmin/raw/main/license.key.gz
/usr/bin/gunzip /tmp/license.key.gz
mv /tmp/license.key /usr/local/directadmin/conf/
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
/usr/sbin/ifup eth0:100
/bin/systemctl restart directadmin.service
```
