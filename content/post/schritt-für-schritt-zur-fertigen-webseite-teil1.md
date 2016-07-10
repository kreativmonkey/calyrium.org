+++
Categories = ["Development", "Webwork"]
Description = ""
Tags = ["Webdesign", "Hugo", "Processwire", "Atom", "Vim", "Sass/SCSS", "Jade"]
date = "2016-07-08T12:41:10+02:00"
menu = "main"
title = "Schritt für Schritt zur fertigen Webseite - Teil 1: Hilfsmittel im Einsatz"

+++
In der Reihe Schritt für Schritt zur fertigen Webseite möchte ich meine Herangehensweise an das Designen neuer Webauftritte
erläutern. Im ersten teil geht es dabei um die Hilfsmittel die ich bei der Entwicklung einsetze und wieso ich sie Verwende. 
Dies soll keinen davon abhalten seine gewohnten Tools weiter zu verwenden sondern lediglich aufzeigen was ich einsetze und 
euch Anregungen geben was es noch so auf dem Markt gibt.

## Tools
Jeder Koch hat seine eigenen Messer, so ist es auch bei den Webworkern. Im folgenden möchte ich auf die Tools und Programme 
eingehen die ich in meinen Projekten verwende. Einige davon könnten euch bekannt vorkommen, andere eher nicht. Ich kann
aus eigener Erfahrung sagen das es sich bewährt hat neues gegenüber offen zu sein und sich ab und an zu trauen etwas
aus zu probieren.

### Atom und Vim
Als Texteditoren dienen mir Atom auf dem Desktop und Vim auf der Konsole. [Atom](www.atom.io) ist noch ein sehr junges Projekt und hat ab und an
ein paar Aussetzer, dennoch ist es meiner Meinung nach für jeden einen Blick wert. 
Es handelt sich dabei um einen Schlichten Texteditor der von [Git]({{< relref "#versionsverwaltung" >}})Hub entwickelt wird. 
Er ist sehr stark an Sublime angelehnt und bietet mit seinem schlichten Design eine gute Arbeitsumgebung bei der man sich voll und ganz
auf den Code konzentrieren kann.

[Vim](www.vim.org) ist ein Texteditor für die Konsole unter Linux, er ist sehr mächtig und hat sich für das schnelle Korrigieren absolut bewerte. 
Ich muss zugeben, es ist schon ein wenig Nerd Stuff aber wer Linux einsetzt oder einen SSH Zugang zu seinem Server/Webhoster benutzt sollte einen
Blick drauf werfen.

Wer mit Atom nicht warm wird, dem kann ich noch [SublimeText 3]() empfehlen. Eine bekannte Größe unter den Webworkern welcher wie Atom wert auf 
Schlichtheit und einfache Erweiterbarkeit bietet.

### Precompiler Jade und Sass
Precompiler sind eine sehr große Hilfe im Webdesign und ich bin froh das ich mich an sie ran getraut habe. 
Sie bringen oft Zusatzfunktionen mit und sind dank ihres minimalistischen Markups meist übersichtlicher und 
besser zu lesen. Die Einarbeitungszeit ist oft nicht so lang wie man anfänglich vermutet und absolut gut investiert.
Alles in allem kann man sagen das man sich mit Hilfe von Precompilern viel Arbeit sparen kann. 

#### Jade
[Jade](http://jade-lang.com/) ist ein Precompiler für HTML und dient mir zum Aufbau der Struktur einer Webseite. 
Der Vorteil ist mehr die Übersichtlichkeit als die kleinen Funktionen die Jade mit bringt. 
Ein kleines Beispiel soll das ganze etwas veranschaulichen:

**HTML Code:**
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>Jade</title>
        <script type="text/javascript">
            if (foo) {
            bar(1 + 5)
            }
        </script>
    </head>
    <body>
        <h1>Jade - node template engine</h1>
        <div id="container" class="col">
            <p>You are amazing</p>
            <p>
              Jade is a terse and simple
              templating language with a
              strong focus on performance
              and powerful features.
            </p>
        </div>
    </body>
</html>
```

**Jade Code:**
```jade
doctype html
html(lang="en")
    head
        title= pageTitle
        script(type='text/javascript').
            if (foo) {
            bar(1 + 5)
            }
        body
            h1 Jade - node template engine
            #container.col
                if youAreUsingJade
                    p You are amazing
                else
                    p Get on it!
                p.
                    Jade is a terse and simple
                    templating language with a
                    strong focus on performance
                    and powerful features.
```

Wie man unschwer erkennen kann ist der Code hierbei viel übersichtlicher und kürzer. Wie gesagt nutze ich Jade lediglich zur Erstellung des Markups aber das erleichtert 
einem schon enorm die Arbeit.

#### Sass / SCSS
[Sass](http://sass-lang.com/) ist ein Prekompiler für CSS Code und erleichtert, dank seiner vielen nützlichen Funktionen wie mixins und variablen, das erstellen
von Umfangreichen Designs. Ob man nun Sass verwendet oder SCSS oder eine Mischung aus beiden, ist dabei jedem selbst überlassen. Aufgrund der geringeren Schreibarbeit
verwende ich mittlerweile nur noch Sass und SCSS kommt nur in Ausnahmefälle zum Einsatz. Ein kleines Beispiel soll die Unterschiede deutlich machen:

**Sass Code:**
```sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
    font: 100% $font-stack
    color: $primary-color
hr
    border-top-color: $primary-color
article
    h1
        a
            color: $primary-color
```

**SCSS Code:**
```SCSS
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
    font: 100% $font-stack;
    color: $primary-color;
}
hr {
    border-top-color: $primary-color;
}
article{
    h1{
        a{
            color: $primary-color;
        }
    }
}
```

**CSS Code:**
```css
body {
    font: 100% Helvetica, sans-serif;
    color: #333;
}
hr {
    border-top-color: #333;
}
article h1 a{
    color: #333;
}
```

Dank der Variable ``$primary-color`` kann man nun sehr einfach die Primäre Schriftfarbe ändern und muss nicht jedes Element in seinem Code suchen und anpassen.
Des weiteren lassen sich verschachtelte Anweisungen viel einfacher und Komfortabler umsetzen und lesen.

### Versionsverwaltung
Mit einem Versionierungssystem hat man die Möglichkeit zu jedem Zeitpunkt seine Änderungen wieder Rückgängig zu machen oder schnell mal eben etwas zu testen. Eine 
bekannte Größe in diesem Bereich ist die OpenSource Versionsverwaltung [Git](https://git-scm.com/). Entwickelt zur Verwaltung des Linux Kernels hat sich Git,
nicht zu letzt dank [GiftHub](https://github.com/), zu einer der beliebtesten Versionsverwaltungs- Programme gemausert. Ich verwende Git bei all meinen Projekten es
das Arbeiten im Team erleichtert und mit wenigen Schritten ein Backup System eingerichtet ist.

### Prepros
Als einziges Kommerzielles Programm das ich gerne einsetze ist [Prepros](https://prepros.io/) in meiner liste die absolute Ausnahme. Das Programm ist für Windows, Mac OS und Linux 
verfügbar und versteht sich als Precompiler. Es bringt alle nötigen Libarys mit und hat noch einige andere nützliche Zusatzfunktionen. 

Prepros überwacht unseren Projektordner auf Änderungen und compiliert die Dateien dann automatisch neu. Mit dem Integrierten Webserver 
kann man die Seite direkt aufrufen und sogar Synchron auf verschiedenen Geräten gleichzeitig anschauen. Erkennt Prepros eine neue Datei 
wird die Seite im Browser automatisch neu geladen. 
Außerdem lassen sich, nach getaner Arbeit, die Änderungen mit einem Mausklick per FTP hochladen.

Viele Features bekommt  man zwar auch mit verschiedenen Konsolen Programmen hin, jedoch erleichtert Prepros den einstieg und Einrichtung und macht dabei eine gute Figur. 

## Hilfsmittel

### Bourbon, Neat und Bitters
Vor kurzem bin ich auf die Sass Mixin Libarys [Bourbon](http://bourbon.io/), [Neat](http://neat.bourbon.io/) und [Bitters](http://bitters.bourbon.io/) gestoßen, 
wobei Bitters keine Libary ist sondern ein Styling für die wichtigsten Elemente einer Webseite mitbringt. 

Bourbon bringt eine Vielzahl an Mixins mit sich die einem viel denk und Schreibarbeit abnimmt. Das ganze spannt sich von vordefinierten 
Variablen für font-family bis hin zu Mixins für vendor Präfixes. 

Neat bietet, im Zusammenspiel mit Bourbon, eine Mixinlibary zur einfachen Umsetzung eines Grid-Layouts. 
Dabei muss das HTML Markup nicht angefasst werden sondern das Styling wird allein mit Hilfe von Sass vorgenommen. 

### Bootstrap, Foundation und andere Frameworks
Wieso das Rad immer wieder neu erfinden, mit Hilfe von [Twitter Bootstrap](http://getbootstrap.com/) oder 
[Zurb Foundation](http://foundation.zurb.com/) lassen sich viele Anwendungen schnell und schick designen.
Ich habe beides lange Zeit eingesetzt bis ich auf Bourbon gestoßen bin. Seit ich Bourbon entdeckt habe wandle ich meine Webprojekte nach und nach zu selbst geschriebenen 
Code um denn alle Frameworks haben eines gemeinsam, sie bringen eine menge Overhead mit sich. Viele Bestandteile eines Frameworks kommen oft gar nicht zum einsatz und 
sind trotzdem im Code vorhanden, das verlängert die Ladezeit und führt teilweise auch zu abstrusem CSS Code wie ich bei anderen Projekten sehen durfte.

### CMS und Statische Webseiten
Lange zeit habe ich für meine Webprojekte [WordPress](https://wordpress.org/) genutzt und war damit auch sehr zufrieden. Zugegeben, wer schnell einen Block aufsetzen möchte der ist mit
WordPress auch heute noch sehr gut bedient, mir Persönlich ging der Wust an Plugins und co. irgendwann sehr auf die Nerven.

Für eines meiner Projekte kam eine Zeitlang dann [Drupal](https://www.drupal.org/) zum einsatz, welches zwar sehr mächtig ist aber ein hohes maß an Einarbeitung benötigt. Nachdem
mein Webprojekt nach zwei Jahren einige Änderungen erhalten sollte habe ich gemerkt das ich alles wieder Vergessen hatte was ich mir vorher angeeignet habe. 
Gefrustet davon habe ich mich auf die suche nach einer anderen Lösung begeben.

Mit [ProcessWire](https://www.processwire.com) habe ich für mich nun das ideale CMS gefunden. Es hat aus meiner Sicht eine eingängliche API, 
bietet einem genau das was man braucht und ist sehr gut auf den jeweiligen Einsatzzweck anpassbar. 
ProcessWire versteht sich als eine Mischung von CMS und CMF (Content Management Framework) da es einem, bei der Ausgabe der 
Daten, absolut freie Hand lässt. Wer eine weile damit gearbeitet hat wird seinen eigenen Workflow finden und kann ProcessWire als Backend für verschiedene Anwendungen 
einsetzen. 

Seit neustem Arbeite ich (wie auch [hier in meinem Blog]({{< ref "migration-zu-hugo.md" >}})) auch mit statischen Webseiten. 
Durch [Hugo](https://gohugo.io) einem statischem Webseiten Generator ist das auch nicht all zu schwierig.
Für das eigene Template muss man sich erst mit der Templatesprache von der Programmiersprache Go vertraut machen. Keine Angst, es klingt schwieriger als es ist. 
Der Vorteil von Hugo gegenüber anderen statischen Seitengeneratoren ist zum einen die Geschwindigkeit und zum anderen die Einfachheit. Zum nutzen genügt es sich 
Hugo herunter zu laden und es gibt keine weiteren Abhängigkeiten die beachtet werden müssen.

## Weiterführende Links
* [Sass für Einsteiger - holgerkoenemann.de](http://www.holgerkoenemann.de/sass-fuer-einsteiger-teil1-hintergruende-installation/)
* [Sass Videotutorial - Unleashed Design](https://www.youtube.com/watch?v=5Yb6MiFSKEQ)
* [Sass für Einsteiger - Bernhard Kau - WordCamp Cologne](https://kau-boys.de/files/2015/06/SASS-f%C3%BCr-Einsteiger.pdf)
* [Atom ausprobiert - golem.de](http://www.golem.de/news/atom-ausprobiert-githubs-konfigurierbarer-editor-ist-vielversprechend-1507-114959.html)
* [ProcessWire Deutschland](http://de.processwire.com/)
* [Einstieg ProcessWire - Webkrauts](http://webkrauts.de/artikel/2012/processwire)
* [Statische Webseiten mit Hugo erzeugen - c't 12/16](http://www.heise.de/ct/ausgabe/2016-12-Statische-Websites-mit-Hugo-erzeugen-3211704.html)

Ich habe mich bei den Links absichtlich auf deutsche Artikel beschränkt da es sich hier um den Einstieg handelt. 
Ich kann jedem nur nahe legen englische Beiträge zu suchen da es davon oft mehr gibt und sie bieten einen größeren Umfang.
