# Aufgabe 06  MIB Browser

## GNS3

![image-20210708110118946](images/image-20210708110118946.png)

Auf den PCs jeweils Ip-Adresse vom dhcp erhalten mit:

```bash
ip dhcp
```

## SNMP Aktivieren

Im webfig von Mikrotik IP > SNMP:

![image-20210708110504633](images/image-20210708110504633.png)

## ipAdEntAddr

![image-20210708110831597](images/image-20210708110831597.png)

Der wert entspricht der IP-Adresse des Routers(192.168.23.170). Der wert ist read-only.

## ifInUcastPkts.2

![image-20210708111002168](images/image-20210708111002168.png)

Dies sind die eintreffenden Unicast Packete auf Port 2. Der Wert kann z.B. durch das Pingen des Routers von PC1 erhöht werden.

Dieser wert kann unter Webfig > Interfaces >  ether2 > Traffic gefunden werden:

![image-20210708111231913](images/image-20210708111231913.png)