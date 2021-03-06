+++
Categories = ["Webwork"]
Description = "Von WordPress zu Hugo, mein Umstieg zur Statischen Webseite."
Tags = ["Development", "golang", "Webseite", "WordPress", "Hugo", "Git"]
date = "2016-06-26T11:42:45+02:00"
draft = false
title = "Migration zur statischen Webseite mit Hugo"

+++
Jahre lang hat mir WordPress mehr oder weniger gute Dienste geleistet. 
Zum einstieg in die Arbeit mit Webseiten hat es mir viele Funktionen 
mit wenig wissen geboten. Mit den Jahren habe ich mich weiter Entwickelt 
und dazu gelernt. Durch die Arbeit an verschiedenen Projekten habe ich 
immer stärker gemerkt das es notwendig ist sich stark Systeme mit vielen 
Plugins zu kümmern. Mit dem steigenden Wissen hatte ich die Möglichkeit 
kleinere Plugins durch eigene Lösungen zu ersetzen. Da jedoch auch die 
Zeit immer knapper wird wollte ich dafür sorgen das ein Verwaltungsaufwand 
weniger existiert. Und was liegt da näher das eine Projekt, meinen Privaten, 
nicht sehr frequentierten Blog von WordPress los zu sagen und auf eine 
statische Webseite zu migrieren.

## Wieso Hugo
In letzter Zeit habe ich vieles über verschiedene statische Webseitengeneratoren 
gehört und mein Interesse war geweckt. Die Systeme Middleman und Jekyll 
haben sich jedoch wegen ihrer vielen Abhängigkeiten direkt selbst disqualifiziert. 
Als ich dann anfing mit Go (golang) zu experimentieren habe ich mich umgeschaut 
welche Projekte damit umgesetzt wurden und bin auf Hugo gestoßen. Ein kleines 
Programm zum generieren von statischen Webseiten. Hugo ist leichtgewichtig und 
lässt sich auf Windows, Mac und Linux betreiben und bietet einige nette Gimmiks 
wie z.B. einen eingebauten Server mit watch Deamon zum Testen auf dem Heimischen PC. 
Noch dazu bringt es alles mit um auf dem System zu laufen und benötigt keine 
weiteren Abhängigkeiten, genau das was ich von einem wartungsarmen System erwarte. 

## Design
Nun habe ich ein wenig damit experimentiert und gemerkt das mir Hugo sehr gut 
gefällt und beschlossen meine Webseite mit Hilfe von Hugo zu erstellen. Für Hugo 
gibt es eine stetig wachsende Auswahl an fertigen Designs, von OnePager über Blogs
bis hin zu Dokumentationen oder Firmenauftritte. Da ich jedoch etwas mehr über das 
System erfahren wollte habe ich mich auch gleich daran gesetzt ein eigenes Design 
zu erstellen. Die Template Sprache ist mit ein wenig Übung nicht sonderlich schwer 
und bietet viele Möglichkeiten. Dynamische Inhalte können mit Javascript realisiert 
werden. 

## Migration von WordPress zu Hugo
Die Migration gestaltete sich leider etwas schwieriger als gehofft. Wer einen Blog 
mit vielen Artikeln pflegt wird einiges an Arbeit investieren müssen um diesen 
einwandfrei zu migrieren. Es gibt ein [Plugin](https://github.com/SchumacherFM/wordpress-to-hugo-exporter) 
zum Export der Artikel zu Hugo welches die Artikel in Markdown exportiert. 
Wer jedoch verschiedene Plugins zur Formatierung verwendet der muss viele der 
Artikel per Hand Nachbearbeiten. Zum Beispiel wurden Code Beispiele oder 
YouTube Videos nicht richtig erkannt und eingebunden. Auch Bilder und co. müssen 
überarbeitet werden. Ist die Arbeit jedoch getan, dann bekommt man dank Hugo 
eine statische Webseite die mit Features wie Code Highlighting aufwartet und 
dafür einen wesentlich geringeren Pflegeaufwand benötigt.

## Verwaltung mit Hilfe von Git
In vielen meiner Projekte arbeite ich mit Git und liebe es. Da Hugo rein 
auf Textdateien Basiert bietet es sich gerade zu an Git zur Verwaltung 
ein zu setzen. Auf meinem Computer befindet sich eine exakte Kopie der 
Webseite somit kann ich problemlos offline Artikel verfassen, mir eine 
Vorschau anzeigen lassen und zum ende das ganze veröffentlichen. Mit 
Hilfe von `git push` wird das Repository auf dem Server aktualisiert 
und durch Hugo automatisch die neuen Seiten erstellt. (Artikel hierzu folgt)

Durch einen gleichzeitigen Upload zu Github habe ich meine Webseite an drei 
verschiedenen Orten abgelegt und brauche mich nicht noch zusätzlich um Backups
zu kümmern.

## Markdown zum Ablenkungsferien schreiben
Einen weiteren Vorteil den ich persönlich in den statischen Webseiten Generatoren
gesehen habe ist das verfassen der Webseiten mit dem Editor der Wahl in Markdown. 
Markdown als Auszeichnungssprache ist sehr einfach zu erlernen und bietet die Anwendung
nicht nur für Statische Webseiten sondern auch für Wikis oder E-Mails lässt es sich
sehr geschickt einsetzen. Ein weiterer Vorteil von Markdown ist, das man die 
Wahl hat mit welchem Editor man die Texte verfassen möchte. Es gibt Onlinetools wie 
[dillinger.io](http://dillinger.io/) welche das Markdown direkt rendern und darstellen,
es genügt jedoch auch ein einfacher Texteditor auf der Kommandozeile. 
Für mich hat es den Vorteil das ich weniger Abgelenkt werde von der Formatierung. Es ist
sehr angenehm sich nicht mit einem Wisywig Editor und seinen Eigenheiten Auseinander 
setzen zu müssen. Ich hoffe dies führt dazu das ich wesentlich häufiger in meinen
Blog schreiben werde.
