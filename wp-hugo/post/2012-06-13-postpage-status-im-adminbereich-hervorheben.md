---
title: Post/Page Status im Adminbereich hervorheben
author: Kreativmonkey
layout: post
date: 2012-06-13
url: /2012/06/13/postpage-status-im-adminbereich-hervorheben/
categories:
  - Wordpress

---
Mit dem Folgenden kleinen Codeschnipsel lässt sich der Status (Entwurf, Geplant, Privat&#8230;) im Adminbereich hervorheben.

Eingefügt wird der Code in die function.php deines Themes:

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
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;">add_action('admin_footer','posts_status_color');
function posts_status_color(){
?&gt;
.status-draft{background: #FCE3F2 !important;}
.status-pending{background: #87C5D6 !important;}
.status-publish{/* no background keep wp alternating colors */}
.status-future{background: #C6EBF5 !important;}
.status-private{background:#F2D46F;}
<span style="color: #000000; font-weight: bold;">&lt;?php</span> 
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

via [WPsnipp.com][1]

 [1]: http://wpsnipp.com/index.php/functions-php/change-admin-postpage-color-by-status-draft-pending-published-future-private/