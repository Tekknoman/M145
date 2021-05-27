# Übung 01

## Aufgabenstellung

Ihr Computer ist über ein Layer 2 VPN mit dem GNS3 Server verbunden. Das hat den Vorteil, dass Sie ohne Routing Ihr virtuelles Netzwerk im GNS3 mit der Aussenwelt, beziehungsweise Ihrem Computer verbinden können. Dafür ist das Subnetz 192.168.23.0/24 vorgesehen. 192.168.23.1/24 ist die Adresse des GNS3 Servers. Ein DHCP Server ist aktiv und hat das IP-Pool 192.168.23.129 – 200.

## Ziele

- Von meinem Computer R2 anpingen
- Auffrischen der IPv4 Routing Kenntnisse
- Erste Erfahrungen mit MikroTik Router OS und GNS3 sammeln

## Parameter

## Generell

| Subnetz A | 192.168.23.0/24   |
| --------- | ----------------- |
| Subnetz B | 192.168.25.0/24   |
| Router OS | MikroTik CHR V6.* |

## R1

| Interface | IP Address     |
| --------- | -------------- |
| ether2    | 192.168.25.1   |
| ehter1    | 192.168.23.133 |

## R2

| Interface | IP Address   |
| --------- | ------------ |
| ether2    | 192.168.25.2 |

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

Output von `ip route print`:

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

Output von `ip route print`:

```bash
 #      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
 0 A S  192.168.23.0/24                    192.168.25.1              1
 1 ADC  192.168.25.0/24    192.168.25.2    ether2                    0
```

## Überprüfung

Wir habe die Richtigkeit der Einstellungen mit Pings von unserem PC aus getestet.

### R1

ether1:

```powershell
ping 192.168.23.133
```

```powershell
Ping wird ausgeführt für 192.168.23.133 mit 32 Bytes Daten:
Antwort von 192.168.23.133: Bytes=32 Zeit=15ms TTL=64
Antwort von 192.168.23.133: Bytes=32 Zeit=7ms TTL=64
Antwort von 192.168.23.133: Bytes=32 Zeit=7ms TTL=64
Antwort von 192.168.23.133: Bytes=32 Zeit=7ms TTL=64

Ping-Statistik für 192.168.23.133:
    Pakete: Gesendet = 4, Empfangen = 4, Verloren = 0
    (0% Verlust),
Ca. Zeitangaben in Millisek.:
    Minimum = 7ms, Maximum = 15ms, Mittelwert = 9ms
```

ether2:

```powershell
ping 192.168.25.1
```

```powershell
Ping wird ausgeführt für 192.168.25.1 mit 32 Bytes Daten:
Antwort von 192.168.25.1: Bytes=32 Zeit=7ms TTL=64
Antwort von 192.168.25.1: Bytes=32 Zeit=7ms TTL=64
Antwort von 192.168.25.1: Bytes=32 Zeit=7ms TTL=64
Antwort von 192.168.25.1: Bytes=32 Zeit=8ms TTL=64

Ping-Statistik für 192.168.25.1:
    Pakete: Gesendet = 4, Empfangen = 4, Verloren = 0
    (0% Verlust),
Ca. Zeitangaben in Millisek.:
    Minimum = 7ms, Maximum = 8ms, Mittelwert = 7ms
```

### R2

ether2:

```powershell
ping 192.168.25.2
```

```powershell
Ping wird ausgeführt für 192.168.25.2 mit 32 Bytes Daten:
Antwort von 192.168.25.2: Bytes=32 Zeit=8ms TTL=63
Antwort von 192.168.25.2: Bytes=32 Zeit=9ms TTL=63
Antwort von 192.168.25.2: Bytes=32 Zeit=9ms TTL=63
Antwort von 192.168.25.2: Bytes=32 Zeit=9ms TTL=63

Ping-Statistik für 192.168.25.2:
    Pakete: Gesendet = 4, Empfangen = 4, Verloren = 0
    (0% Verlust),
Ca. Zeitangaben in Millisek.:
    Minimum = 8ms, Maximum = 9ms, Mittelwert = 8ms
```

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

Route hinzufügen:

```bash
ip route add dst-address=(Zielnetz/CIDR) gateway=(Gateway bzw. Adresse des Interfaces)
```

