+++
Categories = ["Development"]
Description = "Um die eigene Sicherheit beim Surfen in öffentlichen Netzwerken zu erhöhen ist eine VPN Verbindung ein gutes Mittel. Wieso die Aufgabe nicht Automatisieren?"
Tags = ["Tasker", "VPN", "Sicherheit"]
date = "2016-12-02T09:40:20+01:00"
menu = "main"
title = "VPN in öffentlichen Netzen durch Tasker"
+++

Tasker ist eine App für das Smartphone zum Automatisieren von Abläufen. Da sich das Smartphone in der Regel automatisch mit einem bekannten Netzwerk verbindet ist es notwendig das es auch von selbst entscheidet das es einen VPN Tunnel aufbauen muss. Dies ist jedoch nur in öffentlichen Netzwerken der Fall und somit habe ich mir gedanken gemacht wie man das umsetzen kann.

Tasker leistet mir schon seit Jahren sehr gute Dienste und es kommen immer wieder neue Tasks und Profile hinzu die mir das leben leichter machen sollen. So war Tasker auch dieses mal mittel der Wahl. Da es mir zu viel aufwand ist die Liste der privaten und öffentlichen Netze von Hand zu pflegen habe ich das auch automatisiert. Tasker kümmert sich nun beim Verbinden mit einem Netzwerk darum zu schauen ob er das Netzwerk schon kennt und fragt bei bedarf nach.

## Funktionsweise
Zur Umsetzung habe ich 3 Profile eingerichtet, eines für unbekannte Netzwerke, eines für öffentliche Netzwerke und eines für private. Bei einem unbekannten Netzwerk fragt Tsaker zu welcher Kategorie das Netzwerk gehört und speichert dies im jeweiligen Array. Handelt es sich um ein öffentliches Netzwerk dann startet Tasker die VPN Verbindung.

## Umsetzung
Zur Umsetzung wird folgendes benötigt:

* [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm)
* [OpenVPN für Android](https://play.google.com/store/apps/details?id=de.blinkt.openvpn)
* [OpenVPN Tasker Plugin](https://play.google.com/store/apps/details?id=com.ffrog8.openVpnTaskerPlugin)

Zunächst müsst ihr in OpenVPN für Tasker ein [VPN einrichten](http://www.pcwelt.de/ratgeber/Virtuelle-Netzwerke-mit-Open-VPN-aufbauen-9889432.html) das ihr später aktivieren wollt wenn ihr in einem öffentlichen Netz seid.

### Profil 1 - Unknown Network

Das Profil überprüft ob Wifi Verbunden ist und ob es sich hierbei um ein unbekanntes Netzwerk handelt. Wenn dem so ist wird der Task "unknown network" ausgeführt und ein Dialog öffnet sich in dem man das Netzwerk zuordnen kann.

Bedingung 1: `Status -> Netzwerk -> Wifi Verbunden`
    SSID: %PrivateNetwork%OpenNetwork
    Umkehren: Aktivieren

Bedingung 2: `Status -> Netzwerk -> Wifi Verbunden`

#### Task - unknown network

1. Variable -> Variable Setzen -> %connection zu %WIFII
2. Variable -> Variable Aufteilen -> %connection Teiler "
3. Variable -> Variable Setzen -> %ConnectedNetwork zu %connection2 (%connection2 ist die SSID des Verbundenen Netzwerkes)
4. Alarm -> Menü
  Titel: Wifi: %ConnectedNetwork
  Einträge:
  * Privat (Action = Array Push -> %PrivNetArray position 1 wert %ConnectedNetwork)
  * Öffentlich (Action = Arrad Push -> %OpenNetArray position 1 wert %ConnectedNetwork)
5. Variable -> Array Process -> %PrivNetArray typ Remove Duplicates
6. Variable -> Array Process -> %OpenNetArray typ Remove Duplicates
7. Task -> For -> Variable %netzwork Einträge %PrivNetArray()
8. Variable -> Variable Setzen -> %privnet zu %network/ Hinzufügen: Aktiviert
9. Task -> End For
10. Variable -> Variable Setzen -> Name %PrivateNetwork zu %privnet
11. Task -> For -> Variable %network Einträge %OpenNetArray()
12. Variable -> Variable Setzen -> %opennet zu $netzwork/ Hinzufügen: Aktiviert
13. Task -> End For
14. Variable -> Variable Setzen -> Name %OpenNetwork zu $opennet
15. Variable -> Variable Löschen -> Name %ConnectedNetwork

### Profil 2 - OpenNetwork

Bedingung 1: `status -> Netzwerk -> Wifi Verbunden`
SSID: %OpenNetwork

#### Task - OpenNetwork

1. Plugins -> OpenVpn Tasker Plugin
    Konfiguration: auswahl der VPN verbindung die Aufgebaut werden soll.

An dieser Stelle habe ich den Task so geschrieben das er eigentlich das Aktuelle Netzwerk wieder auf Platz 1 im Array setzt damit immer die am häufigst verwendeten Netzwerke ganz vorne stehen. Ob das jedoch einen Unterschied bei der Geschwindigkeit macht weiß ich nicht. Der Task funktioniert auf alle fälle auch ohne diese Einstellung.
#### Exit Task
2. Plugins -> OpenVpn Tasker Plugin
    Konfiguration: Disconnect

### Profil 3 - PrivateNetwork

Bedingung 1: `Status -> Netzwerk -> Wifi Verbunden`
    SSID: %PrivateNetwork

Hier ist es euch überlassen was für Tasks ausgeführt werden sollen. Ich deaktiviere zum Beispiel meine Stromsparprofile und schalte das Handy laut.

Ich würde mich freuen wenn ihr mir einen Kommentar zu diesem Profil in der [Taskergruppe](https://plus.google.com/101620447980386746176/posts/4qjaan93ugc?sfc=true) hinterlassen würdet. Berichtet mir eure Probleme oder Verbessungesvorschläge für diese Umsetzung.
