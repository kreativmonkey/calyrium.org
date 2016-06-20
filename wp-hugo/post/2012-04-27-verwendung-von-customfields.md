---
title: Verwendung von Customfields
author: Kreativmonkey
layout: post
date: 2012-04-27
url: /2012/04/27/verwendung-von-customfields/
categories:
  - Tutorial
  - Wordpress
tags:
  - Anwendung
  - Ausgabe
  - Benutzerdefinierte Felder
  - Custom Fields
  - Wordpress

---
WordPress bietet die Möglichkeit Benutzerdefinierte Felder, sogenannte Customfields zu verwenden. Natürlich lassen sich zu diesem Thema im Netz unzählige Anleitungen finden, jedoch sind die meisten davon nicht vollständig oder schneiden nur einen Teil der Funktionen an.
  
<!--more-->


  
**Custom Filds im Theme aktivieren**

****Die Benutzerdefinierten Felder findest du unter dem Artikeleingabefeld. Teilweise sind sie jedoch auch ausgeblendet, in diesem Fall musst du unter &#8222;Optionen einblenden&#8220; (oben links in der Ecke) einen Hacken vor &#8222;Benutzerdefinierte Felder&#8220; setzen.

[<img class="alignnone size-large wp-image-83" title="Benutzerdefinierte Felder" src="http://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-170044-1024x398.png" alt="" width="584" height="226" srcset="https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-170044-1024x398.png 1024w, https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-170044-300x116.png 300w, https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-170044-500x194.png 500w, https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-170044.png 1196w" sizes="(max-width: 584px) 100vw, 584px" />][1]

**Benutzerdefinierte Felder nutzen
  
** 

Die Custom Fields bestehen aus einer Variablen &#8222;Name&#8220; und dem Wert der übergeben wird. Als Variable wählst du etwas aus das für dich aussagekräftig ist jedoch kein Leerzeichen oder Sonderzeichen hat. Wir möchten in unserem Beispiel eine Quelle mit Hilfe von Custom Fields einfügen, daher nehme ich als Variable quelleText und quelleLink.
  
Unter Wert gibst du den Wert der Variablen ein.

[<img class="alignnone size-large wp-image-86" title="Eingabe von Benutzerdefinierten Felder" src="http://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-174628-1024x479.png" alt="" width="584" height="273" srcset="https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-174628-1024x479.png 1024w, https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-174628-300x140.png 300w, https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-174628-500x234.png 500w, https://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-174628.png 1213w" sizes="(max-width: 584px) 100vw, 584px" />][2]

**_Wichtig:_** Wenn du den Wert nachträglich ändern möchtest brauchst du den Artikel nicht zu Aktualisieren sondern es reicht wenn du das jeweilige Custom Field über &#8222;Aktualisieren&#8220; aktualisierst.

**Ausgabe von Custom Fields**

Die Ausgabe kann über mehrere Wege gelöst werden. Entweder direkt im Template z.B. in der Datei single.php. Dort fügt man, an die Stelle wo der Text ausgegeben werden soll die folgenden Zeilen ein:

<pre class="lang:default decode:true" title="Custom Fields einbinden">&lt;?php echo get_post_meta($post-&gt;ID, 'value', true) ?&gt;</pre>

In unserem Beispiel sieht das ganze dann so aus:

<pre class="lang:default decode:true" title="Beispiel Einbindung">&lt;?php if ( get_post_meta($pots-&gt;ID, 'quelleText', false) : ?&gt;
        &lt;p&gt; Quelle: &lt;br /&gt;
                &lt;a href="&lt;?php echo get_post_meta($post-&gt;ID, 'quelleLink', true) ?&gt;" title="&lt;?php echo get_post_meta($post-&gt;ID, 'quelleText', true) ?&gt;" &gt;
                      &lt;?php echo get_post_meta($post-&gt;ID, 'quelleText', true) ?&gt;
                 &lt;/a&gt;
&lt;?php endif; ?&gt;</pre>

**_Erklärung:_** Ich frage mit if ab ob das Custom Field quelleText einen Wert hat, ist dem der Fall gebe ich die URL und den Text mit Hilfe von echo aus.

**Alternative Ausgabe**

Man kann die Custom Fields auch mit Shortcodes verbinden. Zu Shortcodes werde ich bald ein weiteres Tutorial schreiben.

**Weiterlesen:**

  * [Custom Fields -> WordPress Codex][3]
  * [Tutorial von Frank Bültge][4]

 [1]: http://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-170044.png
 [2]: http://calyrium.org/wp-content/uploads/2012/04/Bildschirmfoto-vom-2012-04-27-174628.png
 [3]: http://codex.wordpress.org/Custom_Fields
 [4]: http://bueltge.de/wordpress-benutzerdefinerte-felder-custom-fields/525/