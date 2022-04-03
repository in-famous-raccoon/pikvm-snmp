# Configuration on PiKVM
## PiKVM enable write mode
`rw`

## Install net-snmp and nano (you can also us vim instead of nano)
`pacman -S net-snmp nano`

## Configure snmpd
#### Paste content from snmpd.conf to /usr/share/snmp/snmpd.conf
`nano /usr/share/snmp/snmpd.conf`

### Paste content from sh file to /opt folder and make executable
`nano /opt/snmp-cpu-temp.sh`
`chmod +x /opt/snmp-cpu-temp.sh`

### Because PiKVM runs in read only mode the script will fail. We need to link the cache file to tmp folder
`rm /var/net-snmp/.snmp-exec-cache #in case the file already exists`
`ln -s /tmp/.snmp-exec-cache /var/net-snmp/.snmp-exec-cache`

#### Restart SNMPD
`systemctl restart snmpd.service`

## PiKVM enable read only mode
`ro`

# Configuration on PRTG WebUI
#### CPU temperature
* Add sensor
* SNMP Custom
* Name = CPU Temp
* OID = .1.3.6.1.2.1.25.1.8
* Channel Name = Temperature
* Unit String = °C
