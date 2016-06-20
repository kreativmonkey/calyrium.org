---
title: Artikel Aufrufe erfassen ohne Plugin
author: Kreativmonkey
layout: post
date: 2012-06-13
url: /2012/06/13/artikel-aufrufe-erfassen-ohne-plugin/
categories:
  - Tutorial
  - Wordpress

---
Aktuell habe ich versucht den Aufruf von Artikel ohne Plugins wie <a title="Link zum Plugin WP-PostViews" href="http://wordpress.org/extend/plugins/wp-postviews/" target="_blank">WP-PostViews</a> zu erfassen. Ich möchte die Artikelaufrufe zählen um in der Sidebar eine Liste der am häufigsten gelesenen Artikel ein zu fügen. Im folgenden habe ich mein Vorgehen erklärt.

Auf der Hilfreichen Webseite <a title="Wordpress Code Snippets" href="http://wpsnipp.com" target="_blank">WPsnipp.com</a> habe ich den entsprechenden Codeschnipsel gefunden den ich zum Zählen der Aufrufe benötige ([WordPress Track post views without a plugin using post meta][1]). Zum speichern der Anzahl nutze ich wie das Plugin die Benutzerdefinierten Felder wodurch ich ohne Probleme die Anzahl der aufrufe die bisher gezählt wurden übernehmen kann.

## Zählen der Artikelaufrufe

Der Folgende Code gehört in die functions.php deines Themes.

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
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">// Funktion zur anzeigen der Aufrufe im Theme</span>
<span style="color: #000000; font-weight: bold;">function</span> getPostViews<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$count_key</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">'post_views_count'</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Beim ersetzen des WP-PostView Plugin muss hier "views" stehen!</span>
    <span style="color: #000088;">$count</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$count</span><span style="color: #339933;">==</span><span style="color: #0000ff;">''</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
        delete_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        add_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'0'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">"0 View"</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #b1b100;">return</span> <span style="color: #000088;">$count</span><span style="color: #339933;">.</span><span style="color: #0000ff;">' Views'</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
<span style="color: #666666; font-style: italic;">// Funktion zum Zaehlen der Aufrufe</span>
<span style="color: #000000; font-weight: bold;">function</span> setPostViews<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$count_key</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">'post_views_count'</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Beim ersetzen des Plugin WP-PostViews muss hier "views" stehen!</span>
    <span style="color: #000088;">$count</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$count</span><span style="color: #339933;">==</span><span style="color: #0000ff;">''</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$count</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;"></span><span style="color: #339933;">;</span>
        delete_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        add_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'0'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span><span style="color: #b1b100;">else</span><span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$count</span><span style="color: #339933;">++;</span>
        update_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$postID</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count_key</span><span style="color: #339933;">,</span> <span style="color: #000088;">$count</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

Nun musst du noch in deiner single.php folgenden Code hinzufügen:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #666666; font-style: italic;">// Zaehlt die Aufrufe des Artikels</span>
          setPostViews<span style="color: #009900;">&#40;</span>get_the_ID<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Um die Anzahl der Aufrufe in den Artikeln Anzuzeigen musst du an die gewünschte Stelle folgenden Code einfügen:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #666666; font-style: italic;">// Anzeige der Aufrufe im Theme</span>
          <span style="color: #b1b100;">echo</span> getPostViews<span style="color: #009900;">&#40;</span>get_the_ID<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

Nun werden die Aufrufe der Artikel gezählt. Möchtest du bestimmte Benutzergruppen von der Zählung ausschließen (z.B. die Administratoren) dann gelingt dir das mit Folgendem Code:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span> <span style="color: #339933;">!</span> current_user_can<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'administrator'</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// Wenn der User nicht Administrator ist dann Zaehlen!</span>
       <span style="color: #666666; font-style: italic;">// Aufrufe Zaehlen</span>
               setPostViews<span style="color: #009900;">&#40;</span>get_the_ID<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span>;
  }</pre>
      </td>
    </tr>
  </table>
</div>

##  Anzeige der Meist gelesenen Artikel

Zur Anzeige der meist gelesen Artikel bietet sich die Sidebar an, daher habe ich hier den Code für ein kleines aber nützliches Widget welches man über die Pluginverwaltung einspielt und aktiviert.

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
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
</pre>
      </td>
      
      <td class="code">
        <pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span>
<span style="color: #666666; font-style: italic;">/*
Plugin Name: Last_Month_Most_Viewed_Posts
Plugin URI: http://calyrium.org
Description: Dieses Plugin erstellt ein Widget für die WordPress Sidebar
Author: Sebastian Preisner
Version: 1.1
Author URI: http://calyrium.org
*/</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">function</span> most_view_display_widget<span style="color: #009900;">&#40;</span><span style="color: #000088;">$args</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #990000;">extract</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$args</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000088;">$tage</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">'30'</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$artikel</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">'5'</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// Filterfunktion erstellen</span>
        <span style="color: #000000; font-weight: bold;">function</span> filter_where<span style="color: #009900;">&#40;</span> <span style="color: #000088;">$where</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">''</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// Artikel der letzten 30 Tage (xx days koennen beliebig geaendert werden.)</span>
            <span style="color: #000088;">$where</span> <span style="color: #339933;">.=</span> <span style="color: #0000ff;">" AND post_date &gt; '"</span> <span style="color: #339933;">.</span> <span style="color: #990000;">date</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'Y-m-d'</span><span style="color: #339933;">,</span> <span style="color: #990000;">strtotime</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'-$tage days'</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">.</span> <span style="color: #0000ff;">"'"</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">return</span> <span style="color: #000088;">$where</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$before_widget</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$before_title</span><span style="color: #339933;">;</span>?<span style="color: #339933;">&</span>gt<span style="color: #339933;">;</span>Top <span style="color: #000088;">$artikel</span> der letzten <span style="color: #000088;">$tage</span> Tage<span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span>?php <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$after_title</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"&lt;ul&gt;"</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// Filter aktivieren</span>
    add_filter<span style="color: #009900;">&#40;</span> <span style="color: #0000ff;">'posts_where'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'filter_where'</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// Abfrage starten</span>
        <span style="color: #000088;">$query</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> WP_Query<span style="color: #009900;">&#40;</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'showposts'</span> <span style="color: #339933;">=&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000ff;">'$artikel'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'orderby'</span> <span style="color: #339933;">=&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000ff;">'meta_value_num'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'meta_key'</span> <span style="color: #339933;">=&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000ff;">'views'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'order'</span> <span style="color: #339933;">=&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000ff;">'DESC'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'category__not_in'</span> <span style="color: #339933;">=&</span>gt<span style="color: #339933;">;</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1799</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">while</span> <span style="color: #009900;">&#40;</span> <span style="color: #000088;">$query</span><span style="color: #339933;">-&</span>gt<span style="color: #339933;">;</span>have_posts<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> <span style="color: #000088;">$query</span><span style="color: #339933;">-&</span>gt<span style="color: #339933;">;</span>the_post<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000088;">$views</span> <span style="color: #339933;">=</span> get_post_meta<span style="color: #009900;">&#40;</span><span style="color: #000088;">$post</span><span style="color: #339933;">-&</span>gt<span style="color: #339933;">;</span>ID<span style="color: #339933;">,</span> <span style="color: #0000ff;">'views'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"&lt;li&gt;"</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"&lt;a href='"</span><span style="color: #339933;">;</span> <span style="color: #b1b100;">echo</span> get_permalink<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"'&gt;"</span><span style="color: #339933;">;</span> <span style="color: #b1b100;">echo</span> get_the_title<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"&lt;/a&gt;"</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"&lt;/li&gt;"</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">endwhile</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">"&lt;/ul&gt;"</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$after_widget</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// Filter deaktivieren (Wichtig!!)</span>
    remove_filter<span style="color: #009900;">&#40;</span> <span style="color: #0000ff;">'posts_where'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'filter_where'</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
        <span style="color: #009933; font-style: italic;">/**
	 * Sanitize widget form values as they are saved.
	 *
	 * @see WP_Widget::update()
	 *
	 * @param array $new_instance Values just sent to be saved.
	 * @param array $old_instance Previously saved values from database.
	 *
	 * @return array Updated safe values to be saved.
	 *
	public function update( $new_instance, $old_instance ) {
		$instance = array();
		$instance['title'] = strip_tags( $new_instance['title'] );
                $instance['number'] = strip_tags( $new_instance['number']);
		return $instance;
	}
&nbsp;
        // Back-End Einstellungen
        public function form( $instance ) {
        if ( isset( $instance[ 'title' ] ) ) {
			$title = $instance[ 'title' ];
		}
		else {
			$title = __( 'New title', 'text_domain' );
		}
        if (isset( $instance[ 'number'] ) ) {
                        $number = $instance[ 'number' ];
        }
            else {
                $number = '5';
            }
		?&gt;
		&lt;p&gt;
		&lt;label for="&lt;?php echo $this-&gt;get_field_id( 'title' ); ?&gt;"&gt;&lt;?php _e( 'Title:' ); ?&gt;&lt;/label&gt; 
		&lt;input class="widefat" id="&lt;?php echo $this-&gt;get_field_id( 'title' ); ?&gt;" name="&lt;?php echo $this-&gt;get_field_name( 'title' ); ?&gt;" type="text" value="&lt;?php echo esc_attr( $title ); ?&gt;" /&gt;
                &lt;label for="&lt;?php echo $this-&gt;get_field_id( 'number' ); ?&gt;"&gt;&lt;?php _e( 'Anzahl:' ); ?&gt;&lt;/label&gt;
                &lt;input class="widefat" id="&lt;?php echo $this-&gt;get_field_id( 'number'); ?&gt;" name="&lt;?php echo $this-&gt;get_field_name( 'nubmber'); ?&gt;" type="text" value="&lt;?php echo esc_attr( $number ); ?&gt;" /&gt;
		&lt;/p&gt;
		&lt;?php 
&nbsp;
        } */</span>
<span style="color: #009900;">&#125;</span>
wp_register_sidebar_widget<span style="color: #009900;">&#40;</span>
    <span style="color: #0000ff;">'mostview_lastmonth_1'</span><span style="color: #339933;">,</span>        <span style="color: #666666; font-style: italic;">// your unique widget id</span>
    <span style="color: #0000ff;">'Most view last month'</span><span style="color: #339933;">,</span>          <span style="color: #666666; font-style: italic;">// widget name</span>
    <span style="color: #0000ff;">'most_view_display_widget'</span><span style="color: #339933;">,</span>  <span style="color: #666666; font-style: italic;">// callback function</span>
    <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span>                  <span style="color: #666666; font-style: italic;">// options</span>
        <span style="color: #0000ff;">'description'</span> <span style="color: #339933;">=&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000ff;">'Zeigt die am häufigsten aufgerufenen Artikel des letzten Monats'</span>
    <span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

&nbsp;

&nbsp;

 [1]: http://wpsnipp.com/index.php/functions-php/track-post-views-without-a-plugin-using-post-meta/