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
| ehter1    | 192.168.23.133 | DHCP     |

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

Den DHCP haben wir ebenfalls über das Webinteface via DHCP Setup konfiguriert:

 

