# cloyne OpenWRT

instant OpenWRT config!

## how to

### flash tl-wr1043nd WAP

- unboxing
  - unbox tl-wr1043nd
  - plug in power to tl-wr1043nd
  - plug in ethernet to tl-wr1043nd (LAN not WAN port) and your computer
- [bootloader downgrade](http://wiki.openwrt.org/toh/tp-link/tl-wr1043nd#bootloader.downgrade)
  - connect to tl-wr1043nd either using DHCP or static ip in 192.168.1.1xx range
  - browse to http://192.168.1.1
  - log in with user `admin` and password `admin`
  - click `System Tools` on the left sidebar
  - click `Firmware Upgrade` on the left sidebar
  - click `Choose File` and browse to `./firmware/tl-1043nd/original.img`
  - click `Upgrade`
- install factory OpenWRT
  - reconnect to tl-wr1043nd either using DHCP or static ip in 192.168.1.1xx range
  - run `./bin/flash ./firmware/tl-1043nd/factory.img`
  - do not unplug anything and wait. the tl-wr1043 will eventually drop your connection, reflash, and reboot.
- generate Cloyne profile
  - run `./bin/tl-1043nd-wap <ip_address> <hw_address> <hostname>`
    - where <ip_address> is in range 192.168.0.2 - 192.168.0.254
    - where <hw_address> is the same hardware addresss on the back of the tl-wr1043nd in form `AA:BB:CC:DD:EE:FF`
    - where <hostname> is in form c1-wap
- install sysupgrade Cloyne profile
  - reconnect to tl-wr1043nd either using DHCP or static ip in 192.168.1.1xx range
  - browse to http://192.168.1.1
  - log in with user `root` and empty password
  - click `System` at top
  - click `Backup / Flash Firmware` at top
  - by `Flash new firmware image`, uncheck `Keep settings`, click `Choose File`, browse to `./ImageBuilder/bin/ar71xx/openwrt-ar71xx-generic-tl-wr1043nd-v1-squashfs-sysupgrade.bin`, click 'Flash image...', verify the md5sum with `cat ./ImageBuilder/bin/ar71xx/md5sums | grep openwrt-ar71xx-generic-tl-wr1043nd-v1-squashfs-sysupgrade.bin`, and proceed!
  - do not unplug anything and wait. the tl-wr1043 will eventually drop your connection, reflash, and reboot.
- find your new WAP at <ip_address>! you will not be able to DHCP through it until it is connected to the main network.

## TODO

change 

`./bin/tl-1043nd-wap <ip_address> <hw_address> <hostname>`

to

`./bin/build -p profiles/tl-1043-wap -i <ip_address> -m <mac_address> -h <hostname>`
