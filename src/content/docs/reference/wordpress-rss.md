---
title: Custom base RSS feed for WordPress
---

Set UTC +3 time zone
```
<?php
header('Content-Type: application/rss+xml; charset=UTF-8');

echo '<?xml version="1.0" encoding="UTF-8" ?>';

?>
<rss version="2.0">
<channel>
    <title><?php echo get_bloginfo('name'); ?></title>
    <link><?php echo get_bloginfo('url'); ?></link>
    <description>Your custom feed description</description>
    <language>en-us</language>

    <?php
    $args = array(
        'post_type' => 'post',  // Fetch posts or any custom post types
        'posts_per_page' => 10  // Limit the number of posts
    );
    $custom_query = new WP_Query($args);

    if ($custom_query->have_posts()) :
        while ($custom_query->have_posts()) : $custom_query->the_post();
    ?>
    <item>
        <title><?php the_title_rss(); ?></title>
        <link><?php the_permalink_rss(); ?></link>
        <description><![CDATA[<?php the_excerpt_rss(); ?>]]></description>
        <pubDate><?php echo date('D, d M Y H:i:s', strtotime(get_the_time('Y-m-d H:i:s') . ' +0 hours')) . ' +0300'; ?></pubDate>
        <?php
        // Get post categories
        $categories = get_the_category();
        if (!empty($categories)) :
            foreach ($categories as $category) :
        ?>
            <category><?php echo $category->name; ?></category>
        <?php
            endforeach;
        endif;
        ?>
        <full-text><![CDATA[
            <?php echo apply_filters('the_content', get_the_content()); ?>
        ]]></full-text>

 <?php if (has_post_thumbnail()) : 
            $thumbnail_url = get_the_post_thumbnail_url(get_the_ID(), 'full'); // Get the featured image URL
            ?>
            <enclosure url="<?php echo esc_url($thumbnail_url); ?>" type="image/jpeg" />
        <?php endif; ?>
        <guid isPermaLink="false"><?php the_guid(); ?></guid>
    </item>
    <?php
        endwhile;
    endif;
    wp_reset_postdata();
    ?>
</channel>
</rss>
```

Creteate a new feed custom.pnpg file in the theme folder.
function.php:

```


function custom_feed_init() {
    add_feed('custom', 'generate_custom_feed');
}
add_action('init', 'custom_feed_init');

function generate_custom_feed() {
    get_template_part('custom');
}

```