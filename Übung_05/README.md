# Aufgabe_05

## Aufgabenstellung

- Verbinden Sie mit einem Ethernet-Kabel einen Laptop der Gruppe mit dem Access Point, geben Sie sich eine statische IP Adresse aus dem Subnet *172.16.92.0/24* und rufen das Webinterface des Gerätes auf (172.16.92.51).
- Versuchen Sie folgende Fragen zu Ihrem Gerät zu beantworten:
<<<<<<< Updated upstream

  1. Welcher Hardware-Typ hat ihr WLAN interface (Marke + Modellnummer)?
  2. Welche Frequenzbänder unterstützt(en) ihr(e) WLAN interface(s)?
  3. Wie viele physischen WLAN interfaces sind auf ihrem Gerät vorhanden?
  4. Was für ein Typ Antenne besitzt ihr Gerät?

=======
  1.  
>>>>>>> Stashed changes
- Aktivieren Sie ihr WLAN interface.
- Scannen Sie mithilfe der Funktion *Scan* des WLAN interfaces das 2.4 GHz Frequenzband ab. Welche Kanäle sind belegt? Verwenden Sie einen WLAN Kanalscanner auf einem Handy oder Laptop. Stellen Sie unterschiede fest?
- Wenn Ihr Gerät 5GHz fähig ist, machen Sie das gleiche für dieses Frequenzband.
- Gibt es hier an der TBZ Access Points, die sich nicht an die optimale Aufteilung auf die Kanäle 1,6,11 halten?
- ügen Sie unter /interface wireless channels für das 2.4GHz Band die drei Kanäle 1,6 und 11 in eine Channel-Liste mit dem Namen *«2.4GHz Channels»* ein.
- Fügen Sie unter /interface wireless channels für das 5GHz Band drei **nicht** **DFS** Kanäle in eine Channel-Liste mit dem namen *«5GHz Channels»* ein.
- Setzen im *Default Security Profile* die Passphrase auf EnteEnteEnte und aktivieren Sie **nur** WPA2.
- Beantworten Sie in Ihrem Laborbericht die Frage, weshalb Sie **WPA** nicht aktivieren sollten.
- Setzen Sie die SSID. Verwenden Sie dazu den Namen Gruppe5:
  Nach dem obligaten Teil dürfen Sie natürlich einen beliebigen Freitext einfügen.
- Wählen Sie für Ihr 2.4 GHz WLAN interface einen vorkonfigurieren *Channel* aus. Koordinieren Sie an der Wandtafel den Kanal. Ziel ist es, dass nicht alle Gruppen den gleichen Kanal verwenden.
- Versuchen Sie sich mit Ihrem Access Point zu verbinden.
   Sehen Sie die SSID?
   Erhalten Sie eine IP-Adresse?
   Dokumentieren Sie Ihre Erkenntnisse im Laborbericht.
- Prüfen Sie mit welcher TX Geschwindigkeit Sie mit dem Access Point verbunden sind. (Screenshot!)
- Beantworten Sie folgende Frage in Ihrem Laborbericht:
   Wie viele Kanäle verwenden Sie? (Laborbericht)
- Versuchen Sie den Access Point so zu konfigurieren, dass Sie zwei Kanäle verwenden.
- Prüfen Sie nochmals Ihre TX Geschwindigkeit.
   Was stellen Sie fest? Notieren Sie Ihre Feststellungen mit Screenshots in Ihrem Laborbericht.
- Fügen Sie ein tagged VLAN interface (VLAN-ID 145) auf einem freien Ethernet Port hinzu.
- Erstellen Sie ein virtuelles WLAN interface mit der SSID wie oben, aber fügen Sie zu beginn noch «Client» ein.
- Erstellen Sie eine virtuelle Bridge und fügen Sie beiden interfaces der vorhergehenden Schritte dieser hinzu.
- Verbinden Sie Ihren Access Point mit dem zentralen Switch.
- Verbinden Sie sich nun mit einem Laptop mit diesem neuen WLAN.
   Erhalten Sie eine IP-Adresse?
   Können Sie sich mit dem Internet verbinden?
   ( Notieren im Laborbericht inkl. Screenshots)
- Wenn Sie nun eine IP Adresse erhalten haben und Zugriff auf das Internet haben sind Sie Fertig .

## Ziele

- Sie können ein sicheres WLAN auf einem WLAN fähigen MikroTik Router konfigurieren
- Sie können mehrere SSIDs auf einem physischen WLAN interface aufschalten.
- Sie können den richtigen Kanal für Ihren Access Point konfigurieren.

## Lösungen / Dokumentation

### Interface Informationen

| Frage          | Antwort                       |
| -------------- | ----------------------------- |
| Hardware-Typ   | Intel(R) Wi-Fi 6 AX200 160MHz |
| Frequenzbänder | 2.4GHz, 5GHz                  |
| Anzahl         | 1                             |
| Antenne        | 2x2                           |

