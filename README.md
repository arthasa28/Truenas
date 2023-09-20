# Truenas

```bash
1. Install zerotier
sed -i .orig 's/enabled: yes/enabled: no/' /usr/local/etc/pkg/repos/local.conf
sed -i .orig 's/enabled: no/enabled: yes/' /usr/local/etc/pkg/repos/FreeBSD.conf
pkg update
pkg install -y zerotier

2.Start the service
service zerotier onestatus
service zerotier onestart

3. Move the database to a persisted zfs dataset
mkdir -p /mnt/tank/zerotier/db/
mv /var/db/zerotier-one/* /mnt/tank/zerotier/db/
/sbin/mount_nullfs /mnt/tank/zerotier/db/ /var/db/zerotier-one
ls -1 /var/db/zerotier-one

4. Join ZeroTier network
zerotier-cli join <NETWORK-ID>
zerotier-cli info
cp /usr/local/etc/rc.d/zerotier /mnt/tank/zerotier/zerotier.rc.d

5.Create the startup script
curl https://alan.norbauer.com/articles/zerotier-on-truenas/scripts/zerotier-start.sh -o /mnt/tank/zerotier/zerotier-start.sh
chmod +x /mnt/tank/zerotier/zerotier-start.sh

6. Add zerotier-start.sh to TrueNAS as a Pre-Init startup script
```
