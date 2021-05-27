# Übung 01

## IP Adressen festlegen

### Auf R1:

IP für Subnetz B setzen:

```bash
ip address add address=192.168.25.1/24 interface=ether2
```

IP für Subnetz A wurde automatisch bezogen.

### Auf R2:

IP für Subnetz B setzen:

```bash
ip address add address=192.168.25.2/24 interface=ether2
```



## Routing

### Auf dem eigenem Gerät:

Damit die Pakete in das Subnetz B an den richtigen Router gesendet werden, muss dies zuerst auf dem eigenen Gerät konfiguriert werden:

Win PS: 

```bash
route add 192.168.25.0 MASK 255.255.255.0 192.168.23.133
```



### Auf R1:

Die Routen sollten bereits automatisch richtig eingestellt sein.

Output von `/ip route print`:

```bash
 #      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
 0 ADC  192.168.23.0/24    192.168.23.133  ether1                    0
 1 ADC  192.168.25.0/24    192.168.25.1    ether2                    0
```



### Auf R2:

Eine Route war bereits richtig konfiguriert. Zusätzlich musste aber die Route in das Subnet A noch hinzugefügt werden:

```bash
ip route add dst-address=192.168.23.0/24 gateway=192.168.25.1
```

Output von `/ip route print`:



## Commands

 Auf die IP-Adressen Einstellungen zugreifen:

```bash
ip address
```

IP Adresse an interface binden:

```bash
ip address add address=(IP-Adresse und CIDR) interface=(Interface)
```

Alle IP-Adressen anzeigen:

```bash
ip address print 
```

 IP-Adresse und Interface löschen:

```bash
ip address remove (nummer)
```
