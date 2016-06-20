---
title: Google Maps Karte einbinden ohne Plugin (API V3)
author: Kreativmonkey
layout: post
date: 2012-04-13
url: /2012/04/13/google-maps-karte-ohne-plugin-api-v3/
categories:
  - Tutorial
  - Wordpress
tags:
  - API V3
  - featured
  - Google
  - Googlemaps
  - Javascript
  - Maps
  - Wordpress

---
Auf [einem meiner Projekte][1] wollte ich eine Google Maps Karte integrieren um die Stellenanzeigen und Events optisch auf zu peppen und den Ort zu Visualisieren. Hierfür kann und möchte ich aus verschiedenen Gründen kein Plugin verwenden. Erstens sind die Plugins nicht immer sauber Programiert und laden den Code an stellen wo es unnütze ist und zweitens tragen verschiedene Kunden die Events und Stellenanzeigen ein und dies macht die Nutzung eines Plugins noch schwieriger.

Leider musste ich feststellen das sich alle Tutorials auf die schon seit 2010 veraltete Google Maps Java API V2 beziehen. Daher habe ich mich entschlossen mir hier gleich mal eine Gedankenstütze zu schaffen falls ich den Code nochmal benötigen sollte.
  
<!--more-->

**Problem:**

  * Einbinden einer Google Map ohne Plugin
  * Verwendung von Custom Fields zur Markierung in der Karte
  * Ausgabe auf den vorgesehenen Seiten.

**Lösung:**

**Vorbereitung der Adresse aus den Custom Fields**
  
Zunächst wollen wir die Adresse aus den Custom Fields herauslesen. Für meine Zwecke sind die Angaben der Adresse in einzelnen Custom Fields unterteilt, somit habe ich ein Feld für die Straße und Hausnummer, Postleizahl sowie den Ort und das Land.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #666666; font-style: italic;">// Adressdaten auslesen $strasse = get_post_meta($post-&gt;ID, 'cpt_strasse_nr', true);</span>
<span style="color: #000088;">$plz</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">ID</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'cpt_postleizahl'</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$ort</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">ID</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'cpt_stadt'</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$land</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">ID</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'cpt_land'</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Und im Folgenden setze ich alles zu einer Adresse zusammen:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #666666; font-style: italic;">// Lokation Informationen zusammenfügen </span>
<span style="color: #000088;">$adresse</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$strasse</span> <span style="color: #339933;">.</span><span style="color: #0000ff;">', '</span><span style="color: #339933;">.</span><span style="color: #000088;">$plz</span> <span style="color: #339933;">.</span><span style="color: #0000ff;">' '</span><span style="color: #339933;">.</span><span style="color: #000088;">$ort</span><span style="color: #339933;">.</span><span style="color: #0000ff;">', '</span><span style="color: #339933;">.</span><span style="color: #000088;">$land</span> <span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Nun sollte die Ausgabe so aussehen: _Musterstraße 12, 99999 Musterhausen, Deutschland_ und ist somit perfekt für den nächsten Schritt.

**Erzeugen der Google Map**
  
Zunächst müssen wir die Google API laden, dies tun wir nicht, wie in den meisten Tutorials beschrieben, im &#8222;Header&#8220; bereich sondern an der Stelle wo die Karte hin soll. Der Vorteil hierbei ist das die JS API nur dort geladen wird, wo wir sie brauchen.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="javascript" style="font-family:monospace;"><span style="color: #339933;">&lt;</span>script type<span style="color: #339933;">=</span><span style="color: #3366CC;">"text/javascript"</span> src<span style="color: #339933;">=</span><span style="color: #3366CC;">"https://maps.google.com/maps/api/js?sensor=false"</span><span style="color: #339933;">&gt;&lt;/</span>script<span style="color: #339933;">&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Nun erzeugen wir die Karte mit einem Marker auf der angegeben Adresse

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
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
</pre>
      </td>
      
      <td class="code">
        <pre class="javascript" style="font-family:monospace;"><span style="color: #339933;">&lt;</span>script type<span style="color: #339933;">=</span><span style="color: #3366CC;">"text/javascript"</span><span style="color: #339933;">&gt;</span>
		<span style="color: #000066; font-weight: bold;">var</span> geocoder<span style="color: #339933;">;</span>
  		<span style="color: #000066; font-weight: bold;">var</span> map<span style="color: #339933;">;</span>
		jQuery<span style="color: #009900;">&#40;</span>document<span style="color: #009900;">&#41;</span>.<span style="color: #660066;">ready</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">function</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
 			initialize<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
			<span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
&nbsp;
  		<span style="color: #000066; font-weight: bold;">function</span> initialize<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			geocoder <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">new</span> google.<span style="color: #660066;">maps</span>.<span style="color: #660066;">Geocoder</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000066; font-weight: bold;">var</span> latlng <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">new</span> google.<span style="color: #660066;">maps</span>.<span style="color: #660066;">LatLng</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">-</span><span style="color: #CC0000;">34.397</span><span style="color: #339933;">,</span> <span style="color: #CC0000;">150.644</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000066; font-weight: bold;">var</span> myOptions <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span>
      				zoom<span style="color: #339933;">:</span> <span style="color: #CC0000;">13</span><span style="color: #339933;">,</span>
      				center<span style="color: #339933;">:</span> latlng<span style="color: #339933;">,</span>
      				mapTypeId<span style="color: #339933;">:</span> google.<span style="color: #660066;">maps</span>.<span style="color: #660066;">MapTypeId</span>.<span style="color: #660066;">ROADMAP</span>
    			<span style="color: #009900;">&#125;</span>
    			map <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">new</span> google.<span style="color: #660066;">maps</span>.<span style="color: #660066;">Map</span><span style="color: #009900;">&#40;</span>document.<span style="color: #660066;">getElementById</span><span style="color: #009900;">&#40;</span><span style="color: #3366CC;">"map_canvas"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> myOptions<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
    			codeAddress<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  			<span style="color: #009900;">&#125;</span>
&nbsp;
		<span style="color: #000066; font-weight: bold;">function</span> codeAddress<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #000066; font-weight: bold;">var</span> address <span style="color: #339933;">=</span> <span style="color: #3366CC;">"&lt;?php echo $adresse; ?&gt;"</span><span style="color: #339933;">;</span>
    			geocoder.<span style="color: #660066;">geocode</span><span style="color: #009900;">&#40;</span> <span style="color: #009900;">&#123;</span> <span style="color: #3366CC;">'address'</span><span style="color: #339933;">:</span> address<span style="color: #009900;">&#125;</span><span style="color: #339933;">,</span> <span style="color: #000066; font-weight: bold;">function</span><span style="color: #009900;">&#40;</span>results<span style="color: #339933;">,</span> status<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
      			<span style="color: #000066; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status <span style="color: #339933;">==</span> google.<span style="color: #660066;">maps</span>.<span style="color: #660066;">GeocoderStatus</span>.<span style="color: #660066;">OK</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        			map.<span style="color: #660066;">setCenter</span><span style="color: #009900;">&#40;</span>results<span style="color: #009900;">&#91;</span><span style="color: #CC0000;"></span><span style="color: #009900;">&#93;</span>.<span style="color: #660066;">geometry</span>.<span style="color: #660066;">location</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        			<span style="color: #000066; font-weight: bold;">var</span> marker <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">new</span> google.<span style="color: #660066;">maps</span>.<span style="color: #660066;">Marker</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#123;</span>
            				map<span style="color: #339933;">:</span> map<span style="color: #339933;">,</span>
            				position<span style="color: #339933;">:</span> results<span style="color: #009900;">&#91;</span><span style="color: #CC0000;"></span><span style="color: #009900;">&#93;</span>.<span style="color: #660066;">geometry</span>.<span style="color: #660066;">location</span>
        			<span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      			<span style="color: #009900;">&#125;</span> <span style="color: #000066; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
        			alert<span style="color: #009900;">&#40;</span><span style="color: #3366CC;">"Geocode was not successful for the following reason: "</span> <span style="color: #339933;">+</span> status<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  		<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #339933;">&lt;/</span>script<span style="color: #339933;">&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Hier möchte ich noch einmal den Wichtigen Part herausnehmen und erläutern:

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
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;">function codeAddress() {
    			var address = "<span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$adresse</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span>";
    			geocoder.geocode( { 'address': address}, function(results, status) {
      			if (status == google.maps.GeocoderStatus.OK) {
        			map.setCenter(results[0].geometry.location);
        			var marker = new google.maps.Marker({
            				map: map,
            				position: results[0].geometry.location
        			});
      			} else {
        			alert("Geocode was not successful for the following reason: " + status);
      			}</pre>
      </td>
    </tr>
  </table>
</div>

Mit Hilfe des vom Google eigenen Dienst [Geocoding][2] ermitteln wir mit Hilfe der Adresse den Längen und Breitengrad der zur Darstellung der Karte benötigt wird. Bei _var adresse=&#8220; &#8222;;_ übergeben wir die aus den Custom Fields zusammengesetzte Adresse. Durch _var marker = new google.maps.Marker._ wird ein [Marker][3] auf die Adresse gesetzt.

**Ausgabe der Karte**
  
Mit dem folgenden Codefragment lässt sich die Karte dann auf eurer Webseite ausgeben:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #339933;">&lt;</span>div id<span style="color: #339933;">=</span><span style="color: #0000ff;">"map_canvas"</span> style<span style="color: #339933;">=</span><span style="color: #0000ff;">"width:100%; height:300px;"</span><span style="color: #339933;">&gt;&lt;/</span>div<span style="color: #339933;">&gt;&lt;!--</span> <span style="color: #666666; font-style: italic;">#map_canvas --&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Dieser Teil muss dort hin wo die Karte ausgegeben werden soll. Die größe lässt sich wie von einem Div gewohnt mit den Parametern width und height anpassen, davor und danach kann alles stehen was du willst, nur nicht in dem Div!
  
Alternativ: [Google Maps als Shortcode][4]

**Zusammenfassung**
  
Hier möchte ich dir nochmal den Code an einem Stück präsentieren, du brauchst ihn nur Kopieren und an der Gewünschten stelle ein zu fügen. Vergiss bitte nicht die Variablen der Custom Fields an zu passen!

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
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #666666; font-style: italic;">// Adressdaten auslesen $strasse = get_post_meta($post-&gt;ID, 'cpt_strasse_nr', true);</span>
<span style="color: #000088;">$plz</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">ID</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'cpt_postleizahl'</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$ort</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">ID</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'cpt_stadt'</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$land</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">ID</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'cpt_land'</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #666666; font-style: italic;">// Lokation Informationen zusammenfügen 	</span>
<span style="color: #000088;">$adresse</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$strasse</span> <span style="color: #339933;">.</span><span style="color: #0000ff;">', '</span><span style="color: #339933;">.</span><span style="color: #000088;">$plz</span> <span style="color: #339933;">.</span><span style="color: #0000ff;">' '</span><span style="color: #339933;">.</span><span style="color: #000088;">$ort</span><span style="color: #339933;">.</span><span style="color: #0000ff;">', '</span><span style="color: #339933;">.</span><span style="color: #000088;">$land</span> <span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span>
&nbsp;
&lt;!-- Google Maps Script einbinden --&gt;
&lt;script type="text/javascript" src="https://maps.google.com/maps/api/js?sensor=false"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
		var geocoder;
  		var map;
		jQuery(document).ready(function() {
 			initialize();
			}); 
&nbsp;
  		function initialize() {
    			geocoder = new google.maps.Geocoder();
    			var latlng = new google.maps.LatLng(-34.397, 150.644);
    			var myOptions = {
      				zoom: 13,
      				center: latlng,
      				mapTypeId: google.maps.MapTypeId.ROADMAP
    			}
    			map = new google.maps.Map(document.getElementById("map_canvas"), myOptions);
&nbsp;
    			codeAddress();
  			}
&nbsp;
		function codeAddress() {
    			var address = "<span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$adresse</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span>";
    			geocoder.geocode( { 'address': address}, function(results, status) {
      			if (status == google.maps.GeocoderStatus.OK) {
        			map.setCenter(results[0].geometry.location);
        			var marker = new google.maps.Marker({
            				map: map,
            				position: results[0].geometry.location
        			});
      			} else {
        			alert("Geocode was not successful for the following reason: " + status);
      			}
    		});
  		}
&nbsp;
&lt;/script&gt;
&lt;div id="map_canvas" style="width:100%; height:300px;"&gt;&lt;/div&gt;&lt;!-- #map_canvas --&gt;</pre>
      </td>
    </tr>
  </table>
</div>

**Hinweis:** WordPress hat ein Problem mit dem $-Zeichen, dieses muss man durch jQuery ersetzen ansonsten erhält man ein &#8222;Property &#8218;$&#8216; of object [object DOMWindow] is not a function&#8220;!

 [1]: http://www.mta-r.de/events/
 [2]: https://developers.google.com/maps/documentation/javascript/geocoding
 [3]: https://developers.google.com/maps/documentation/javascript/overlays#Markers
 [4]: http://wpschnipsel.de/2012/07/23/google-maps-shortcode-mit-api-3/