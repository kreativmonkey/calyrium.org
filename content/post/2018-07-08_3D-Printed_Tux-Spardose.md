+++
title = "Vom Code zur Tux-Spardose"
date= 2018-06-09
tags = ["3D-Print", "Tux", "Moneybox", "Spardose", "Variable", "LUG-MYK", "Linux", "PLA", "OpenSCAD"]
keywords = ["3D-Print", "Tux", "Moneybox", "Spardose", "Variable", "LUG-MYK", "Linux", "PLA", "OpenSCAD"]
categories = ["Linux", "DIY"]
postimage = "/images/tux-moneybox/tux-final.JPG"
description = "Mit OpenSCAD, 3D-Druck, Farbe und Pinsel zu einer Tux-Spardose für unsere LUG."
author = "kreativmonkey"
aliases = ["/posts/vom-code-zur-tux-spardose"]
+++

Seit einigen Jahren suchen wir für unsere Linux Usergroup (LUG) eine Spardose in Form eines Tux. Leider scheint der Markt hierfür nicht groß genug zu sein. Dank der 3D-Drucktechnik lassen sich solche Objekte mittlerweile auch gut selbst fertigen. Nur hat sich niemand finden können der die Fähigkeit und Zeit zur Erstellung einer solchen Spardose hatte. 
Auch mir fehlte jegliche Zeit mich in die, doch recht komplizierten, 3D-Tools einzuarbeiten. Vor kurzem habe ich dann [OpenSCAD](http://www.openscad.org/) entdeckt. Hierbei handelt es sich um eine CAD Software bei der man die Objekte codet und nicht mit der Maus und vielen Tastenkürzeln erstellt. Im ersten Moment klingt das alles andere als einfach, es stellt sich jedoch heraus, dass man dadurch das Programm viel schneller erlernt. 

## Tux-Spardose
Nach ein wenig Einarbeitung habe ich mir also ein Projekt gesucht um das Programm noch besser kennen zu lernen. Was bietet sich da besser an als etwas, dass man sowieso haben möchte. Also machte ich mich auf die Suche nach einer Vorlage von einem Tux für OpenSCAD. Nach kurzer Suche bin ich bei [runeman](http://www.runeman.org/3d/tux/) fündig geworden. Der Code bot eine ganz solide Basis. Nun galt es die Vorlage zu verfeinern und dann in eine Spardose umzuwandeln. 

![Tux RAW in OpenSCAD](/images/tux-moneybox/tux-openscad.png  "Tux in OpenSCAD")

Zunächst habe ich den Code modularisiert und parametrisiert, damit ich den Tux mit einer Variable in seiner Größe verändern kann. Durch die Modularisierung konnte ich nun den Innenraum erzeugen und von der Figur abziehen. Im weiteren Verlauf habe ich den Code soweit angepasst, dass man auch die Wandstärke einstellen und somit auch die Arme und Füße aushölen kann. 

## Der erste Druck

![Printing Process](/images/tux-moneybox/tux-print.gif  "Tux Printing Process")

Bei einem Kollegen konnte ich den Tux in Auftrag geben. Dieser hat ihn mit einem UltiMaker2 gedruckt. Die Höhe betrug 0,1mm mit einem Düsendurchmesser von 0,4mm. Die Druckgeschwindigkeit lag bei ca. 40mm/s. Hierbei lag die Druckzeit bei langen 96 Stunden. 

Der Tux lässt sich, bis auf eine kleine Stütze in der mitte (für den obersten Teil des Kopfes), ohne Stützmaterial drucken. Die Einstellungen sorgten für einen sehr detailierten Druck mit einer relativ glatten Oberfläsche. Durch das schwarze Filament müsste man dem Tux nur geringfügig Farbe angedeihen lassen. Wieso ich mich dann doch umentschieden habe und auch dazu rate, erkläre ich später.

![Tux nach dem Druck](/images/tux-moneybox/tux-after-3D-printing.JPG  "Tux nach dem Druck")

Ich war sehr erstaunt und zufrieden mit dem Ergebnis. Vorallem das mein erstes 3D Objekt nicht nur druckbar sondern auch noch funktionstüchtig war. 

## Fehlerkorrektur und Erweiterung
Aber was wäre ein Druck ohne Fehler? Naklar, ein Druck aus dem man nicht lernt ;-). Also auch hier gab es eine kleine Macke. Zwar habe ich zu beginn nach den Münzgrößen geschaut, jedoch war meine Toleranz nicht groß genug um das Zusammenziehen des Filaments beim Abkühlen auszugleichen. Somit kann die erste Version keine 2 Euro-Münzen aufnehmen.

Den Fehler mit der Schlitzgröße für die Münzen habe ich mit einem größeren Schlitz behoben und hoffe das es nun ausreicht. Aber der Tux soll ja nicht nur im Eurobereich genutzt werden können. Somit habe ich auch gleich Pfund und Dollar mit eingearbeitet. Hierbei muss jedoch die Minimalgröße des Tux selbst beachtet werden da sonst der Hals zu klein ist für die Münzen. 

![Geldschlitz](/images/tux-moneybox/tux-detail-head.JPG  "Geldschlutz")

## Der letzte Anstrich
Eine Tuxspardose ist zwar aus dem Drucker gekommen, jedoch sollte man den Tux für den richtigen Look auch noch Farbe verpassen. Ich habe hierfür einfach Acrylfarbe ([Basic Acryl von Marabu](https://amzn.to/2m2Fr7t)) verwendet. Im Makerspace habe ich von einem Maker eine transparente Grundierung bekommen, damit soll die Farbe besser an dem PLA haften. Als ich diese aufgesprüht habe, war der Tux jedoch an einigen stellen grau (siehe das erste Foto unter diesem Abschnitt am Bauch). Anscheinend hatte ich dort einen zu geringen Abstand beim Sprühen. 

![Beginn des ersten Anstrischs](/images/tux-moneybox/tux-begin-painting.jpg  "Beginn des ersten Anstrischs")

![Die erste Schicht](/images/tux-moneybox/tux-first-layer.jpg  "Die erste Schicht")

Nun blieb mir nichts anderes übrig, ich musste den Tux auch schwarz anmalen. Jedoch kann ich im Nachhinein nur jedem empfehlen das gesamte Objekt zu bemalen. Die durch den Druck bedingten Oberflächenunebenheiten werden durch die Farbe überdeckt und es ergibt sich ein viel gleichmäßigeres Bild. Auch lassen sich dadurch Fehler beim Bemalen der anderen Flächen einfacherer retuschieren. 

![Die 3. Farbschicht](/images/tux-moneybox/tux-3-layer.JPG  "Die 3. Farbschicht")

Für meinen Tux hat es 2 (Schwarz) bis 5 (Gelb) Anstriche, je nach Farbton gebraucht. Natürlich kann man auch schon früher aufhören. In den Fotos kann man den Verlauf der Anstriche etwas verfolgen.

![Nach 4-5 Anstrichen ist er fertig](/images/tux-moneybox/tux-final.JPG  "Nach 4-5 Farbschichten ist er fertig!")

![Tux von unten mit Verschluss](/images/tux-moneybox/tux-detail-bottom.JPG  "Tux von unten mit Verschluss")

## Ausblick
Den Code habe ich auf [Github](https://github.com/kreativmonkey/tux-moneybox) zur Verfügung gestellt. Leider ist es nicht so einfach einen 96 Stunden slot am 3D-Drucker zu erhalten, weswegen ich die neue Version noch nicht testen konnte. Die Druckzeit hat sich durch die Anpassungen zwar verringert, fraglich ist jedoch welche Auswirkungen diese auf die Stabilität haben. Jeder ist gerne dazu eingeladen den Code zu testen und anzupassen. 

Eine Anpassung die ich demnächst noch einarbeiten möchte, ist die Verschönerung des Kopfes. Die Form ist noch nicht perfekt, wobei sich das durch die Bemalung ein wenig verliert.
