---
title: Post/Page Status im Adminbereich hervorheben
author: Kreativmonkey
date: 2012-06-13
url: /2012/06/13/postpage-status-im-adminbereich-hervorheben/
categories:
  - Webwork
tags:
  - Wordpress
  - Snipped
  - Tipps
  - NoPlugin
---
Mit dem Folgenden kleinen Codeschnipsel lässt sich der Status (Entwurf, Geplant, Privat&#8230;) im Adminbereich hervorheben.

Eingefügt wird der Code in die function.php deines Themes:

```php
add_action('admin_footer','posts_status_color');
function posts_status_color(){
?>
.status-draft{background: #FCE3F2 !important;}
.status-pending{background: #87C5D6 !important;}
.status-publish{/* no background keep wp alternating colors */}
.status-future{background: #C6EBF5 !important;}
.status-private{background:#F2D46F;}
<?php 
}
```

via [WPsnipp.com][1]

 [1]: http://wpsnipp.com/index.php/functions-php/change-admin-postpage-color-by-status-draft-pending-published-future-private/
