# cloudtrust-common
========================

## Clone cloudtrust-common repository
```Bash
dnf install -y  cockpit-kdump cockpit-docker cockpit-selinux cockpit-kubernetes
cd /cloudtrust
git clone git@github.com:cloudtrust/cloudtrust-common.git
```

# Io-scheduler
## Clean install
```Bash
systemctl stop io-scheduler.service
systemctl disable io-scheduler.service

rm -fv /etc/systemd/system/io-scheduler.service
rm -fv /etc/systemd/sysctl.d/cloudtrust.conf

rm -rfv /cloudtrust/cloudtrust-common

```
## Install
```Bash

cd /cloudtrust/cloudtrust-common
install -v -m0644 -D deploy/common/etc/systemd/system/io-scheduler.service /etc/systemd/system/io-scheduler.service
install -v -m0644 -D deploy/common/etc/sysctl.d/cloudtrust.conf /etc/sysctl.d/cloudtrust.conf

systemctl enable io-scheduler.service
systemctl start io-scheduler.service
```

# Telegraf
## Clean install
```Bash
systemctl stop telegraf.service
systemctl disable telegraf.service

rm -fv /etc/telegraf/telegraf.conf

dnf remove -y telegraf

rm -rfv /cloudtrust/cloudtrust-common

```

## Install
```Bash
dnf install -y https://dl.influxdata.com/telegraf/releases/telegraf-1.4.4-1.x86_64.rpm

cd /cloudtrust/cloudtrust-common
install -v -m0644 -D deploy/common/etc/telegraf/telegraf.conf /etc/telegraf/telegraf.conf

systemctl daemon-reload
systemctl enable telegraf.service
systemctl start telegraf.service
```
