+++
Categories = ["Development", "GoLang"]
Description = ""
Tags = ["Development", "golang"]
date = "2016-07-09T17:38:28+02:00"
menu = "main"
title = "Schritt für Schritt zur fertigen Webseite - Teil 2 Projekt Strukturieren"

+++
In diesem Teil der Serie Schritt für Schritt zur fertigen Webseite geht es um die Strukturierung des Projekts. 
Häufig ist es so das man einfach mal anfängt und am ende hat man das Chaos komplett. 
Bei einem Webprojekt ist es jedoch sehr einfach eine klare Linie zu fahren da der Ablauf und die benötigten Dateien meist die selben sind.
In diesem Teil wollen wir auf die benötigten Dateien und deren Strukturierung klären, am Ende erhalten wir ein Starter-Kit von dem aus wir immer loslegen können.

## Ordnung muss sein
Im [ersten Teil]({{< ref "schritt-für-schritt-zur-fertigen-webseite-teil1.md" >}}) habe ich euch erklärt mit den Tools und Hilfsmittel die ich verwende Vertraut gemacht.
Nun wollen wir daraus einen Startpunkt für unser Webprojekt erstellen. Hierzu nehme ich das [HTML5 Boilerplate]() als Vorlage und werde mir nachher einzelne Dateien daraus Kopieren.
Zunächsteinmal legen wir einen Ordner für unser Projekt an. 
Innerhalb des Projektordners lege ich nun die folgenden Ordner an, eine Erklärung folgt im Nachhinein.

```
- CSS
- img
- js
- sass
|- 1-tools
|- 2-base
|- 3-plugins
|- 4-layouts
```

Ich denke die Ordner **CSS**, **img** und **js** sind selbsterklärend, sie enthalten jeweils die dateien ihres Typs. 

### Sass Ordner
Innerhalb des Sass Ordners befinden sich die Ortner tools, base, plugins und layouts, jeweils mit einer führenden Ziffer. 
Diese Ziffer soll die Rangfolge verdeutlichen und den Workflow noch ein wenig unterstützen.

Im Ordner **1-Tools** befinden sich alle Sass/SCSS dateien die man von Extern einbindet. 
Hier kommen alse die Dateien von Frameworks, Libarys oder vorgefertigter Code wie [Normalize.css]() rein. 
In meinem Fall enthält dieser Ordner Bourbon, Neat, Bitter und normalize.scss

Der Ordner **2-base** dient uns als platz für alle dateien die grundlegende einstellungen enthalten. 
So erstelle ich dort immer eine Datei _var.sass welche alle Variablen enthält wie z.B. Schriftart, Farbschema, größen Angaben.

Unter **3-plugins** sammel ich die Dateien die spezielle teile einer Webseite definieren. Das kann z.B. eine Timeline oder eine Bildergallerie sein.
Aber auch Code denn ich z.B. unter dem Projekt [Refills](http://refills.bourbon.io/) gefunden habe werden an dieser stelle in einer Datei eingefasst.

Das beste zum Schluss **4-layouts**, hier enthalten sind so dinge wie Blog oder Artikel layout und natürlich dateien für Anpassungen an bestimmten Seiten. 

Diese Struktur erlaubt es mir relativ schnell und einfach den gewünschten bereich der Webseite zu ändern. Gibt es z.B. probleme in der Darstellung des 
Kommentarbereichs weiß ich das ich die dazugehörige datei unter dem Ordner 3-plugins finden werde. Teils sind die Grenzen etwas schwimmend, 
jeder muss hier seine eigenen Erfahrungen machen.

### Tipp für große Projekte
Bei sehr großen Projekten bietet es sich an alle Dateien die auf dem Server landen in einem Ordner ``Public`` zu bündeln. 
Hierbei bleiben die Ordner **js** und **img** im Projektordner zusätzlich bestehen da hier die RAW daten hinein kommen welche, im optimalfall, durch automatisierte Processe vor der Veröffentlichung bearbeitet werden. 
Z.B. das Minifizieren und Bündeln von Javascript Dateien oder das Optimieren der Bilder fürs Web.
Die Ordner werden dann wie folgt aufgebaut:

```
- public
|- css
|- img
|- js
- js
- img
- sass
|- 1-tools
|- 2-base
|- 3-plugins
|- 4-layouts
```

## Dateien

Als nächstes legen wir die benötigten Dateien an. Fangen wir mit dem Projektordner an. Hier kopieren wir uns aus dem HTML5 Boilerplate die folgenden Dateien:

```
404.html
apple-touch-icon.png
favicon.ico
.htaccess
```

aus der index.html erstellen wir mit Hilfe von "[HTML2Jade]()" eine Jade-Datei die wir im Projektordner ablegen.

Danach befüllen wir den Sass-Ordner mit Inhalt. Zunächst legen wir in jedem der 4 Ordner eine Datei namens ``_index.sass`` an, hier werden später die Dateien aus dem jeweiligen Ordner gebündelt importiert. Danach legen wir, direkt im Sass-Ordner, noch eine Datei namens ``app.sass`` an mit dem folgenden Inhalt:

```sass
@import 1-tools/index
@import 2-base/index
@import 3-plugins/index
@import 4-layouts/index
```
Nun organisieren wir uns die Libarys und Framworks die wir verwenden wollen und fügen sie unter 1-tools hinzu. 
In meinem Fall sind das die Libarys "[Bourbon](http://bourbon.io/)" und "[Neat](http://neat.bourbon.io/)" sowie "[Bitters](http://bitters.bourbon.io/)". 
Bourbon und Neat sind reine Libarys welche kein eigenes CSS importieren. 
Bitters hingegen fügt CSS für die Formatierung der wichtigsten HTML Elemente hinzu und benötigt zur korrekten Funktion noch [Normalize.css](https://necolas.github.io/normalize.css/) welches wir auch direkt dort anlegen.

Danach sollte unser Projektordner wie folgt aussehen:

```
- CSS
- img
- js
- sass
|- 1-tools
||- base
||- bitters
||- neat
||- normalize.scss
||- _index.sass
|- 2-base
||- _index.sass
|- 3-plugins
||- _index.sass
|- 4-layouts
||- _index.sass
|- app.sass
- index.jade
- 404.html
- apple-touch-icon.png
- favicon.ico
- .htaccess
```

## Versionierung
Wenn ihr nun eine Versionsverwaltung verwenden wollt dann könnt ihr an dieser Stelle den Ordner Initiieren. 
Setzt ihr Git ein dann macht ihr das indem ihr im Terminal zu eurem Projektordner wechseln und dort ``git init`` eingebt. 
Mithilfe von ``git add -A`` und ``git -m "Init"`` initiiert ihr die Dateien.


## Vorgefertigt

