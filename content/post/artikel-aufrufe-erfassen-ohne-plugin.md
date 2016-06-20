+++
Categories = [
    "WordPress", 
    "Tutorial",
    "Develop"
    ]
Description = "In diesem Artikel geht es darum wie man selbst die Artikelaufrufe in WordPress erfasst ohne ein zusätzliches Plugin von vexern zu integrieren."
Tags = [
    "Development", 
    "WordPress",
    "No Plugin",
    "Artikelaufrufe"
    ]
date = "2012-06-13T14:33:55Z"
title = "Wordpress: Artikel aufrufe erfassen ohne plugin"
author = "Kreativmonkey"

+++
Aktuell habe ich versucht den Aufruf von Artikel ohne Plugins wie [WP-PostViews](http://wordpress.org/extend/plugins/wp-postviews/ "Link zum Plugin WP-PostViews") zu erfassen. Ich möchte die Artikelaufrufe zählen um in der Sidebar eine Liste der am häufigsten gelesenen Artikel ein zu fügen. Im folgenden habe ich mein Vorgehen erklärt.

Auf der Hilfreichen Webseite [WPsnipp.com](http://wpsnipp.com "Wordpress Code Snippets") habe ich den entsprechenden Codeschnipsel gefunden den ich zum Zählen der Aufrufe benötige ([Wordpress Track post views without a plugin using post meta](http://wpsnipp.com/index.php/functions-php/track-post-views-without-a-plugin-using-post-meta/)). Zum speichern der Anzahl nutze ich wie das Plugin die Benutzerdefinierten Felder wodurch ich ohne Probleme die Anzahl der aufrufe die bisher gezählt wurden übernehmen kann.

## Zählen der Artikelaufrufe

Der Folgende Code gehört in die functions.php deines Themes.

```php
// Funktion zur anzeigen der Aufrufe im Theme
function getPostViews($postID){
    $count_key = 'post_views_count'; // Beim ersetzen des WP-PostView Plugin muss hier "views" stehen!
    $count = get_post_meta($postID, $count_key, true);
    if($count==''){
        delete_post_meta($postID, $count_key);
        add_post_meta($postID, $count_key, '0');
        return "0 View";
    }
    return $count.' Views';
}
// Funktion zum Zaehlen der Aufrufe
function setPostViews($postID) {
    $count_key = 'post_views_count'; // Beim ersetzen des Plugin WP-PostViews muss hier "views" stehen!
    $count = get_post_meta($postID, $count_key, true);
    if($count==''){
        $count = 0;
        delete_post_meta($postID, $count_key);
        add_post_meta($postID, $count_key, '0');
    }else{
        $count++;
        update_post_meta($postID, $count_key, $count);
    }
}
```

Nun musst du noch in deiner single.php folgenden Code hinzufügen:

```php
<?php setPostViews(get_the_ID()); //Zaehlt die Aufrufe des Artikels ?>
```

Um die Anzahl der Aufrufe in den Artikeln Anzuzeigen musst du an die gewünschte Stelle folgenden Code einfügen:

```php
<?php echo getPostViews(get_the_ID()); // Anzeige der Aufrufe im Theme  ?-->
```

Nun werden die Aufrufe der Artikel gezählt. Möchtest du bestimmte Benutzergruppen von der Zählung ausschließen (z.B. die Administratoren) dann gelingt dir das mit Folgendem Code:

```php
<?php 
if ( ! current_user_can('administrator') ){ // Wenn der User nicht Administrator ist dann Zaehlen! 
    setPostViews(get_the_ID()); // Aufrufe Zaehlen  
}
?>

```


## Anzeige der Meist gelesenen Artikel

Zur Anzeige der meist gelesen Artikel bietet sich die Sidebar an, daher habe ich hier den Code für ein kleines aber nützliches Widget welches man über die Pluginverwaltung einspielt und aktiviert.

```php
<?php
/*
   Plugin Name: Last_Month_Most_Viewed_Posts
   Plugin URI: http://calyrium.org
   Description: Dieses Plugin erstellt ein Widget für die WordPress Sidebar
   Author: Sebastian Preisner
   Version: 1.1
   Author URI: http://calyrium.org
 */

function most_view_display_widget($args) {
    extract($args);

    $tage = '30';
    $artikel = '5';
    // Filterfunktion erstellen
    function filter_where( $where = '' ) {
        // Artikel der letzten 30 Tage (xx days koennen beliebig geaendert werden.)
        $where .= " AND post_date > '" . date('Y-m-d', strtotime('-$tage days')) . "'";
        return $where;
    }
    echo $before_widget;
    echo $before_title;?>Top $artikel der letzten $tage Tage<?php echo $after_title;
    echo "<ul>";
    // Filter aktivieren
    add_filter( 'posts_where', 'filter_where' );
    // Abfrage starten
    $query = new WP_Query( array('showposts' => '$artikel', 'orderby' => 'meta_value_num', 'meta_key' => 'views', 'order' => 'DESC', 'category__not_in' => array(1799) ) );
    while ( $query->have_posts() ) : $query->the_post();
    $views = get_post_meta($post->ID, 'views');
    echo "<li>";
    echo "<a href='"; echo get_permalink(); echo "'>"; echo get_the_title(); echo "</a>";
    echo "</li>";
    endwhile;
    echo "</ul>";
    echo $after_widget;
    // Filter deaktivieren (Wichtig!!)
    remove_filter( 'posts_where', 'filter_where' );

    /**
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
    ?>
    <p>
    <label for="<?php echo $this->get_field_id( 'title' ); ?>"><?php _e( 'Title:' ); ?></label> 
    <input class="widefat" id="<?php echo $this->get_field_id( 'title' ); ?>" name="<?php echo $this->get_field_name( 'title' ); ?>" type="text" value="<?php echo esc_attr( $title ); ?>" />
    <label for="<?php echo $this->get_field_id( 'number' ); ?>"><?php _e( 'Anzahl:' ); ?></label>
    <input class="widefat" id="<?php echo $this->get_field_id( 'number'); ?>" name="<?php echo $this->get_field_name( 'nubmber'); ?>" type="text" value="<?php echo esc_attr( $number ); ?>" />
    </p>
    <?php 

    } */
}
wp_register_sidebar_widget(
        'mostview_lastmonth_1',        // your unique widget id
        'Most view last month',          // widget name
        'most_view_display_widget',  // callback function
        array(                  // options
            'description' => 'Zeigt die am häufigsten aufgerufenen Artikel des letzten Monats'
            )
        );
```
