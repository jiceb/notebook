# wordpress

* [CPT](#cpt)



## CPT

### Admin

Add sortable columns for a CPT

```php
<?php

/**
 * Add the columns
 */
add_filter('manage_edit-[CPT]_columns', function ( $columns ) {
    $columns['date_start'] = __('Date Start', '[DOMAIN]');
    $columns['date_end'] = __('Date End', '[DOMAIN]');

    return $columns;
} );

/**
 * Make the columns sortable
 */
add_filter( 'manage_edit-[CPT]_sortable_columns', function ( $columns ) {
    $columns['date_start'] = 'date_start';
    $columns['date_end'] = 'date_end';
 
    return $columns;
} );

/**
 * Add the columns content
 */
add_action( 'manage_[CPT]_posts_custom_column', function ( $column_name, $post_id ) {
    $format = 'd/m/Y';
    $columns = array('date_start', 'date_end');

    if( ! in_array($column_name, $columns) ) {
        return;
    }

    if( $column_name == 'date_start' ) {
        echo date($format, strtotime( get_post_meta($post_id, 'date_start', true) ) );
    }elseif( $column_name == 'date_end' ) {
        echo date($format, strtotime( get_post_meta($post_id, 'date_end', true) ) );
    }

}, 10, 2 );

/**
 * Apply sort
 */
add_action( 'pre_get_posts', function ( $query ) {
    if( ! is_admin() ) {
        return;
    }
 
    $orderby = $query->get( 'orderby');
 
    if( 'date_start' == $orderby ) {
        $query->set('meta_key','date_start');
        $query->set('orderby','meta_value_num');

    }elseif( 'date_end' == $orderby ) {
        $query->set('meta_key','date_end');
        $query->set('orderby','meta_value_num');
    }

} );
```
