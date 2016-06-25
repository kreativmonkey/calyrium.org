---
title: Google Maps Karte einbinden ohne Plugin (API V3)
author: Kreativmonkey

date: 2012-04-13
url: /2012/04/13/google-maps-karte-ohne-plugin-api-v3/
categories:
  - Tutorial
  - WordPress
tags:
  - API V3
  - featured
  - Google
  - Googlemaps
  - Javascript
  - Maps
  - WordPress

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

```php
<?php // Adressdaten auslesen $strasse = get_post_meta($post->ID, 'cpt_strasse_nr', true);
$plz = get_post_meta($post->ID, 'cpt_postleizahl', true);
$ort = get_post_meta($post->ID, 'cpt_stadt', true);
$land = get_post_meta($post->ID, 'cpt_land', true); ?>
```

Und im Folgenden setze ich alles zu einer Adresse zusammen:

```php
<?php // Lokation Informationen zusammenfügen 
$adresse = $strasse .', '.$plz .' '.$ort.', '.$land ; ?>
```

Nun sollte die Ausgabe so aussehen: _Musterstraße 12, 99999 Musterhausen, Deutschland_ und ist somit perfekt für den nächsten Schritt.

**Erzeugen der Google Map**
  
Zunächst müssen wir die Google API laden, dies tun wir nicht, wie in den meisten Tutorials beschrieben, im &#8222;Header&#8220; bereich sondern an der Stelle wo die Karte hin soll. Der Vorteil hierbei ist das die JS API nur dort geladen wird, wo wir sie brauchen.

```php
<script type="text/javascript" src="https://maps.google.com/maps/api/js?sensor=false"></script>
```

Nun erzeugen wir die Karte mit einem Marker auf der angegeben Adresse

```php
<script type="text/javascript">
		var geocoder;
  		var map;
		jQuery(document).ready(function() {
 			initialize();
			}); 
 
  		function initialize() {
    			geocoder = new google.maps.Geocoder();
    			var latlng = new google.maps.LatLng(-34.397, 150.644);
    			var myOptions = {
      				zoom: 13,
      				center: latlng,
      				mapTypeId: google.maps.MapTypeId.ROADMAP
    			}
    			map = new google.maps.Map(document.getElementById("map_canvas"), myOptions);
 
    			codeAddress();
  			}
 
		function codeAddress() {
    			var address = "<?php echo $adresse; ?>";
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
 
</script>
```

Hier möchte ich noch einmal den Wichtigen Part herausnehmen und erläutern:

```php
function codeAddress() {
    			var address = "<?php echo $adresse; ?>";
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
```

Mit Hilfe des vom Google eigenen Dienst [Geocoding][2] ermitteln wir mit Hilfe der Adresse den Längen und Breitengrad der zur Darstellung der Karte benötigt wird. Bei _var adresse=&#8220; &#8222;;_ übergeben wir die aus den Custom Fields zusammengesetzte Adresse. Durch _var marker = new google.maps.Marker._ wird ein [Marker][3] auf die Adresse gesetzt.

**Ausgabe der Karte**
  
Mit dem folgenden Codefragment lässt sich die Karte dann auf eurer Webseite ausgeben:

```php
<div id="map_canvas" style="width:100%; height:300px;"> </div><!-- #map_canvas -->
```

Dieser Teil muss dort hin wo die Karte ausgegeben werden soll. Die größe lässt sich wie von einem Div gewohnt mit den Parametern width und height anpassen, davor und danach kann alles stehen was du willst, nur nicht in dem Div!
  
Alternativ: [Google Maps als Shortcode][4]

**Zusammenfassung**
  
Hier möchte ich dir nochmal den Code an einem Stück präsentieren, du brauchst ihn nur Kopieren und an der Gewünschten stelle ein zu fügen. Vergiss bitte nicht die Variablen der Custom Fields an zu passen!

```php
<?php // Adressdaten auslesen $strasse = get_post_meta($post->ID, 'cpt_strasse_nr', true);
$plz = get_post_meta($post->ID, 'cpt_postleizahl', true);
$ort = get_post_meta($post->ID, 'cpt_stadt', true);
$land = get_post_meta($post->ID, 'cpt_land', true); ?>
 
<?php // Lokation Informationen zusammenfügen 	
$adresse = $strasse .', '.$plz .' '.$ort.', '.$land ; ?>
 
<!-- Google Maps Script einbinden -->
<script type="text/javascript" src="https://maps.google.com/maps/api/js?sensor=false"></script>
<script type="text/javascript">
		var geocoder;
  		var map;
		jQuery(document).ready(function() {
 			initialize();
			}); 
 
  		function initialize() {
    			geocoder = new google.maps.Geocoder();
    			var latlng = new google.maps.LatLng(-34.397, 150.644);
    			var myOptions = {
      				zoom: 13,
      				center: latlng,
      				mapTypeId: google.maps.MapTypeId.ROADMAP
    			}
    			map = new google.maps.Map(document.getElementById("map_canvas"), myOptions);
 
    			codeAddress();
  			}
 
		function codeAddress() {
    			var address = "<?php echo $adresse; ?>";
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
 
</script>
<div id="map_canvas" style="width:100%; height:300px;"></div><!-- #map_canvas -->
```

**Hinweis:** WordPress hat ein Problem mit dem $-Zeichen, dieses muss man durch jQuery ersetzen ansonsten erhält man ein &#8222;Property &#8218;$&#8216; of object [object DOMWindow] is not a function&#8220;!

 [1]: http://www.mta-r.de/events/
 [2]: https://developers.google.com/maps/documentation/javascript/geocoding
 [3]: https://developers.google.com/maps/documentation/javascript/overlays#Markers
 [4]: http://wpschnipsel.de/2012/07/23/google-maps-shortcode-mit-api-3/
