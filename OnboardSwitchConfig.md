# On-chip Switch Configuration #

A configuration block needs to be added manually to /etc/config/network. Please login via SSH and edit this file, adding:
```
config switch
    option name 'eth0'
    option reset '1'
    option enable_vlan '1'

config switch_vlan
    option device 'eth0'
    option vlan '1'
    option ports '0 1 2 3 4'
```

And run the following to reload the networking configuration:
```bash

/etc/init.d/network restart```

Then refresh the web management page, you'll see a "Switch" under "Network" menu. Enter and configure what you need if you want to use VLAN, etc...