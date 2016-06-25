---
title: Links aus einem Artikel filtern und am ende Ausgeben
author: Kreativmonkey

date: 2012-08-06
url: /2012/08/06/links-aus-einem-artikel-filtern-und-am-ende-ausgeben/
categories:
  - Tutorial
  - Webwork
tags:
  - Wordpress
  - auslesen
  - ersetzen
  - Filtern
  - pre_match_all
  - pre_metch
  - regex
  - Suchpattern
  - URL

---
Heute habe ich bei wpde.org eine Frage nach einem &#8222;Artikel-link-Crawler&#8220; gelesen. Darunter konnte ich mir erst nicht viel vorstellen. Zur Erklärung, gesucht wurde die Möglichkeit alle im Artikel befindlichen Links heraus zu filtern und am ende des Artikels aus zu geben. Ganz ähnlich findet dies auch bei Wikipedia statt, sobald man eine Quelle zu einer Aussage angibt wird diese am ende der Webseite angezeigt. Nun gut und schön, wer diese Funktion benötigt sucht vergebens, jedoch jetzt nicht mehr. Ich habe mich diesem Problem angenommen und einen kleinen Codeschnipsel dazu verfasst welcher genau das tut was gesucht wurde.

Einfügen in die functions.php des WordPress Themes:

```php
function get_post_urls($content) {
    if( preg_match_all("#((https?://|ftp://|www\.|[^\s:=]+@www\.).*?[a-z_\/0-9\-\#=&])(?=(\.|,|;|\?|\!)?(\"|'|«|»|\[|\s|\r|\n|$))#iS", $content, $url) ) {
        $ausgabe = '<h3>Links zum Artikel</h3>';
        $ausgabe .= '<ul>';
        foreach ($url[0] as $url) {
            $ausgabe .= '<li>'.$url.'</li>';
        }
        $ausgabe .= '<ul>';

        return $content.$ausgabe;
    } else {
        return $content;
    }
}
add_filter('the_content', 'get_post_urls');
```

Die Schwierigkeit hierbei ist es die URL&#8217;s korrekt zu erkennen. Das Suchmuster muss hierzu sehr komplex aufgebaut sein um möglichst wenig fehler zu zu lassen. Wie umfangreich solche suchmuster werden können zeigt der Artikel &#8222;[In search of the perfect URL validation regex][1]&#8222;. Hier findet man Suchmuster von 38 Zeichen bis hin zu 969 Zeichen welche auf den Prüfstand geschickt wurden.

<!--more-->

### Recherche Links

  * http://net.tutsplus.com/tutorials/other/8-regular-expressions-you-should-know/
  * http://www.phpwelt.net/handbuecher/deutsch/function.preg-match-all.html
  * http://www.html-world.de/program/php\_art\_8.php

 [1]: http://mathiasbynens.be/demo/url-regex
