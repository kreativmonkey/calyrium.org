---
title: WordPress mit kleinen Tricks vor Angriffen schützen
author: Kreativmonkey
layout: post
date: 2012-10-18
url: /2012/10/18/wordpress-mit-kleinem-trick-vor-angriffen-schuetzen/
categories:
  - Wordpress
tags:
  - Datenbank
  - Login
  - Sicherheit
  - Wordpress
  - wpdb

---
In meinen etwas besser besuchten Projekten habe ich fast täglich Login versuche auf den User &#8222;admin&#8220; welchen ich natürlich gar nicht erst angelegt habe. Als jedoch das erste mal ein Angriff auf meinen Benutzernamen aufgetreten ist bin ich aufgewacht und habe nach einem Weg gesucht meine WordPress Installation sicherer zu machen. Dabei wollte ich den Komfort nicht einbüßen und einen unbekannten User für die Administration anlegen um jedes mal nachdenken zu müssen mit welchem ich nun schreiben darf oder nicht&#8230;. Die folgende Lösung ist sehr einfach umzusetzen und noch dazu sicher.

Beim anschauen der wp\_user Datenbank ist mir aufgefallen das der Loginname (user\_login) separat gespeichert wird.

[<img class="aligncenter size-full wp-image-382" src="http://calyrium.org/wp-content/uploads/2012/10/user_login.png" alt="" />][1]

Das Problem, beim anlegen eines Users wird der Loginname auch gleich in der Autor URL abgelegt, hierdurch kann man relativ einfach den Loginnamen herausfinden und mit einer Brude Force Attacke versuchen den Account zu knacken.

[<img class="aligncenter size-full wp-image-384" src="http://calyrium.org/wp-content/uploads/2012/10/user_author_url.png" alt="" />][2]

Durch das verändern des Loginnamen in der wp_user Datenbank (z.B. anhängen einer Zahlenkette) lässt sich der Loginname vor außenstehende Verbergen und ist ab sofort so geheim wie es das Passwort sein sollte.

[<img class="aligncenter size-full wp-image-385" src="http://calyrium.org/wp-content/uploads/2012/10/user_login_aendern.png" alt="" />][3]

**<span style="color: #ff0000">Vorsicht</span>: **Hier darfst du kein Leerzeichen oder umlaute verwenden!

**Fazit:**

Mit diesem Weg kann man relativ einfach sein WordPress Backend etwas sicherer machen und das ohne an Komfort ein zu büßen. Natürlich solltest du dich danach mit deinem neuen Namen einloggen.

 [1]: http://calyrium.org/wp-content/uploads/2012/10/user_login.png
 [2]: http://calyrium.org/wp-content/uploads/2012/10/user_author_url.png
 [3]: http://calyrium.org/wp-content/uploads/2012/10/user_login_aendern.png