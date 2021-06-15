# Übung_03

## Aufgabenstellung

- Netzwerk Nach Abbildung im GNS3 nachbauen

- Definieren Sie für jede Abteilung eine VLAN Nummer (VLAN-ID) nach folgendem Shema: 

  | Subnetz          | 192.168.23.0/24                  |
  | ---------------- | :------------------------------- |
  | VLAN Buchhaltung | Gruppennummer 4 * 100 + 1  = 401 |
  | VLAN Entwicklung | Gruppennummer 4 * 100 + 2  = 402 |
  | VLAN Verkauf     | Gruppennummer 4 * 100 + 3  = 403 |

- Definieren Sie für jedes Gerät in den VLANS eine IP-Addresse im gleichen Subnetz.
- Richten Sie die VLANs auf beiden Switches ein
- Führen Sie tests durch um sicherzustellen dass sich nur Geräte aus dem selben VLAN erreichen können.
- Führen Sie auf dem Trunk einen "package capture" aus und analysieren Sie die einzelnen Ethernet Frames

## Ziele

- Auf beiden Switches sind die drei VLANs konfiguriert.
- Die beiden Switches sind über eine Trunk Leitung miteinander verbunden.
- Alle Pings können korrekt ausgeführt werden (im selbern VLAN).
- VLAN Tag mit Wireshark für alle drei VLANs nachgewiesen.
