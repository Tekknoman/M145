# Übung 02

## Aufgabenstellung

- Duplizieren Sie in GNS3 Ihr funktionierendes Projekt von Übung 1.
- Erstellen Sie auf R2 eine virtuelle Bridge und fügen Sie Ports ether3, ether4 und ether5 hinzu.
- Weisen Sie der Bridge die kleinste Adresse von Subnetz C hinzu (Host min).
- Geben Sie den beiden VPCS eine IP-Adresse aus Subnetz C.

## Ziele

- Sie können virtuelle Bridges in MikroTik OS konfigurieren.

- Sie wissen wie man VPCS als Testclients einsetzt.
- Beide VPCS können R1 anpingen.

## Parameter

Grundlage aus [Übung 01](https://github.com/EloiMusk/M145/tree/prod/Übung_01#parameter)

### Generell

| Subnetz A | 192.168.23.0/24   |
| --------- | ----------------- |
| Subnetz B | 192.168.54.0/24   |
| Subnetz C | 192.168.104.0/24  |
| Router OS | MikroTik CHR V6.* |

### R1

| Interface | IP Address     |          |
| --------- | -------------- | -------- |
| ether2    | 192.168.54.1   | Statisch |
| ehter1    | 192.168.23.136 | DHCP     |

### R2

| Interface                        | IP Address    |          |
| -------------------------------- | ------------- | -------- |
| ether2                           | 192.168.54.2  | Statisch |
| bridge1 (ether3, ether4, ether5) | 192.168.104.1 | Statisch |

## Bridge

Die Virtuelle Bridge haben wir über das Webinterface von R2 erstellt.

### Bridge erstellen

Als erstes mussten wir eine Bridge erstellen:

![Overview Bridges](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/bridge_overview.png)

Dort haben wir die Einstellungen vorerst bei den Default Einstellungen belassen.

### Prots Hinzufügen

Anschliessend mussten wir die gewünschten Ports der Bridge zuweisen:

![Overview Ports](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/ports_overview.png)

### Bridge überprüfen

Um die Richtigkeit der Einstellungen zu überprüfen, haben wird die Konfiguration der zuvor hinzugefügten Bridge nochmals angeschaut und konnten dort alle Ports vorfinden (da wir nur 2 VPCs angeschlossen haben werden nur 2 Ports als "Designated angezeigt"):

![Bridged ports](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/bridge_ports.png)

## DHCP

### Auf R2

Den DHCP haben wir ebenfalls über das Webinteface via DHCP Setup konfiguriert:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/dhcp.png)

Die richtige Bridge auswählen:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/dhcp.1.png)

Adessbereich angeben:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/dhcp.2.png)

Gateway festlegen:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/dhcp.3.png)

DHCP Relay (keine angabe):

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/dhcp.4.png)

### Auf VPCs

Die VPCs müssen nun eine Netzwerkkonfiguration vom DHCP anfordern.

Dies geht wie folgt (in der Konsole der VPCs):

```bash
dhcp
```

bzw.

```bash
ip dhcp
```

## Routing

Damit nun alle Pakete aus und in Subnetz C Richtig geroutet werden, muss dies noch eingestellt werden. Alle anderen Routing Einträge sollten bereits on [Übung 01](https://github.com/EloiMusk/M145/tree/prod/Übung_01#routing) noch richtig konfiguriert sein.

### Auf meinem eigenen Gerät:

```powershell
route add 192.168.104.0 MASK 255.255.255.0 192.168.23.136
```

### Auf R1

```bash
ip route add dst-address=192.168.104.0/24 gateway=192.168.54.2
```

### Auf R2

```bash
ip route add dst-address=192.168.23.0/24 gateway=192.168.54.1
```

## Überprüfung

### R1

#### R1 --> VPC:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/R1-vpc.png)

#### R1 --> R2 (Subnetz C bzw. Bridge):

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/r1-r2.png)

### R2

#### R2 --> VPC:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/R2-vpc.png)

### VPC

#### VPC --> R1:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/vpc-r1.png)

#### VPC --> R2 (Subnetz B bzw. ether2):

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/vpc-r2b.png)

#### VPC --> R2 (Subnetz C bzw. bridge):

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/vpc-r2c.png)

#### Netzwerkkonfiguration über dhcp erhalten:

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/dhcp.vpc.png)

### Labor

![](https://github.com/EloiMusk/M145/blob/prod/%C3%9Cbung_02/Images/Labor.png)

## Router Config Export

### R1

```bash
# may/31/2021 03:05:08 by RouterOS 6.47
# software id =
#
#
#
/interface ethernet
set [ find default-name=ether1 ] disable-running-check=no
set [ find default-name=ether2 ] disable-running-check=no
set [ find default-name=ether3 ] disable-running-check=no
set [ find default-name=ether4 ] disable-running-check=no
set [ find default-name=ether5 ] disable-running-check=no
set [ find default-name=ether6 ] disable-running-check=no
set [ find default-name=ether7 ] disable-running-check=no
set [ find default-name=ether8 ] disable-running-check=no
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/ip address
add address=192.168.54.1/24 interface=ether2 network=192.168.54.0
/ip dhcp-client
add disabled=no interface=ether1
/ip route
add distance=1 dst-address=192.168.104.0/24 gateway=192.168.54.2
```

### R2

```bash
# may/31/2021 03:05:57 by RouterOS 6.47
# software id =
#
#
#
/interface bridge
add name=bridge1
/interface ethernet
set [ find default-name=ether1 ] disable-running-check=no
set [ find default-name=ether2 ] disable-running-check=no
set [ find default-name=ether3 ] disable-running-check=no
set [ find default-name=ether4 ] disable-running-check=no
set [ find default-name=ether5 ] disable-running-check=no
set [ find default-name=ether6 ] disable-running-check=no
set [ find default-name=ether7 ] disable-running-check=no
set [ find default-name=ether8 ] disable-running-check=no
/interface wireless security-profiles
set [ find default=yes ] supplicant-identity=MikroTik
/ip pool
add name=dhcp_pool0 ranges=192.168.104.2-192.168.104.254
/ip dhcp-server
add address-pool=dhcp_pool0 disabled=no interface=bridge1 name=dhcp1
/interface bridge port
add bridge=bridge1 interface=ether3
add bridge=bridge1 interface=ether4
add bridge=bridge1 interface=ether5
/ip address
add address=192.168.54.2/24 interface=ether2 network=192.168.54.0
add address=192.168.104.1/24 interface=bridge1 network=192.168.104.0
/ip dhcp-client
add disabled=no interface=ether1
/ip dhcp-server network
add address=192.168.104.0/24 dns-server=8.8.8.8 gateway=192.168.104.1
/ip route
add distance=1 dst-address=192.168.23.0/24 gateway=192.168.54.1
```

