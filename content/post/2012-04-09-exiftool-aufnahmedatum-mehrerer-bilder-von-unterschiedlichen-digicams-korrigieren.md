---
title: ExifTool – Aufnahmedatum mehrerer Bilder von unterschiedlichen Digicams korrigieren
author: Kreativmonkey
layout: post
date: 2012-04-09
url: /2012/04/09/exiftool-aufnahmedatum-mehrerer-bilder-von-unterschiedlichen-digicams-korrigieren/
categories:
  - Fotografie
  - Linux
  - Tutorial
tags:
  - Digikam
  - ExifTool
  - featured
  - Fotografieren
  - Sommerzeit
  - Winterzeit
  - Zeit
---
Kennst du das auch? Zurück von einem schönen Ausflug steckt man die Kamera an den Computer um die Fotos anzuschauen und in die Fotoverwaltung zu kopieren. Da merkt man das die Uhrzeit auf den Fotos nicht passt da man bei der Umstellung am vergangenen Sonntag die Kamera vergessen hat. Ganz doof wird es wenn man die Fotos mit Koordinaten aus einem GPS Tracker synchronisieren möchte. Aber auch für dieses Problem findet sich in der Linuxwelt abhilfe. Mit dem Konsolenprogramm ExifTool und den richtigen parametern lässt sich nicht nur die Zeit korrigieren.
  
<!--more-->

Vor ein paar Tagen ist es wieder einmal so weit gewesen. Einen ganzen lieben langen Tag habe ich Fotografiert und nicht bemerkt das die Kamera noch auf Winterzeit gestellt war (aktuell Sommerzeit). Im Prinzip auch nicht tragisch, jedoch beim Organisieren einer großen Fotodatenbank ist es notwendig das diese Daten stimmen. Vorallem in diesem Fall wollte ich die Bilder mit GPS Koordinaten versehen, welche aus einem GPS Tracker stammen&#8230;.
  
Unter Linux habe ich das Programm ExifTool gefunden mit dem man unter anderem die Zeitinformationen von Bildern korrigieren kann.

zunächst einmal muss du ExifTool installieren, dies machst du am besten auch gleich auf der Konsole mittels folgenden befehl:

```bash
# Ubuntu, Debian und co.
sudo apt-get install libimage-exiftool-perl perl-doc
# Fedora
sudo yum install perl-Image-ExifTool
#Archlinux
sudo pacman -S perl-image-exiftool
```

Das Tool lässt sich nur über die Konsole bedienen und bietet eine Vielzahl an Funktionen. So kann man die Bilder umbenennen, ihnen ein anderes Datum zuweisen oder eben die Zeit anpassen.

In meinem Fall musste ich der im Bild gespeicherten Zeit 1 Stunde drauf rechnen um sie auf Sommerzeit um zu stellen.

```bash
exiftool -AllDates+=01:00 Pfad_zu_den_Bildern/*.JPG
```

**Quellen:**

  * [ExifTool – Aufnahmedatum über die Konsole bedienen und][1][mehrerer Bilder von unterschiedlichen Digicams korrigieren | loggn.de – Tutorials und Erfahrungen][1].
  * [Ubuntuusers Wiki][2]

 [1]: http://www.loggn.de/exiftool-aufnahmedatum-mehrerer-bilder-von-unterschiedlichen-digicams-korrigieren/
 [2]: http://wiki.ubuntuusers.de/ExifTool
