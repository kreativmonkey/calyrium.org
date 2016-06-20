---
title: Links aus einem Artikel filtern und am ende Ausgeben
author: Kreativmonkey
layout: post
date: 2012-08-06
url: /2012/08/06/links-aus-einem-artikel-filtern-und-am-ende-ausgeben/
categories:
  - Tutorial
  - Wordpress
tags:
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

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">function</span> get_post_urls<span style="color: #009900;">&#40;</span><span style="color: #000088;">$content</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #990000;">preg_match_all</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">"#((https?://|ftp://|www\.|[^\s:=]+@www\.).*?[a-z_\/0-9\-\#=&])(?=(\.|,|;|\?|\!)?(<span style="color: #000099; font-weight: bold;">\"</span>|'|«|»|\[|\s|<span style="color: #000099; font-weight: bold;">\r</span>|<span style="color: #000099; font-weight: bold;">\n</span>|$))#iS"</span><span style="color: #339933;">,</span> <span style="color: #000088;">$content</span><span style="color: #339933;">,</span> <span style="color: #000088;">$url</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$ausgabe</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">'&lt;h3&gt;Links zum Artikel&lt;/h3&gt;'</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$ausgabe</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">'&lt;ul&gt;'</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">foreach</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$url</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;"></span><span style="color: #009900;">&#93;</span> <span style="color: #b1b100;">as</span> <span style="color: #000088;">$url</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000088;">$ausgabe</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">'&lt;li&gt;'</span><span style="color: #339933;">.</span><span style="color: #000088;">$url</span><span style="color: #339933;">.</span><span style="color: #0000ff;">'&lt;/li&gt;'</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000088;">$ausgabe</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">'&lt;ul&gt;'</span><span style="color: #339933;">;</span>
&nbsp;
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$content</span><span style="color: #339933;">.</span><span style="color: #000088;">$ausgabe</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span> <span style="color: #b1b100;">else</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$content</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
add_filter<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'the_content'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'get_post_urls'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

Die Schwierigkeit hierbei ist es die URL&#8217;s korrekt zu erkennen. Das Suchmuster muss hierzu sehr komplex aufgebaut sein um möglichst wenig fehler zu zu lassen. Wie umfangreich solche suchmuster werden können zeigt der Artikel &#8222;[In search of the perfect URL validation regex][1]&#8222;. Hier findet man Suchmuster von 38 Zeichen bis hin zu 969 Zeichen welche auf den Prüfstand geschickt wurden.
  
<!--more-->

### Recherche Links

  * http://net.tutsplus.com/tutorials/other/8-regular-expressions-you-should-know/
  * http://www.phpwelt.net/handbuecher/deutsch/function.preg-match-all.html
  * http://www.html-world.de/program/php\_art\_8.php

 [1]: http://mathiasbynens.be/demo/url-regex