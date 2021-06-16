---
id: add-wpseo-opengraph-images-filter
title: Yoast SEO - Allows to alter an existing OpenGraph image
sidebar_label: Alter an existing OpenGraph image
custom_edit_url: https://github.com/Yoast/developer-docs/edit/master/docs/customization/yoast-seo/filters/add-wpseo-opengraph-images-filter.md
---
The filter allows to alter an existing OpenGraph image. If an `og:image` already exists for the page/post/archive, it is replaced by the new one returned by the filter. If there is no `og:image`, nothing is done by the filter.

## Usage

### Alter the OpenGraph image for a single post
```php
<?php
/**
 * Alter the OpenGraph image for a single post
 */
function alter_existing_opengraph_image( $image ) {
    $image_id = $an_image_id;
    $post_id = $a_post_id;
    if ( is_single( $post_id ) ) {
        $image = wp_get_attachment_image_src( $image_id )[0];
    }
    return $image;
}
add_filter( 'wpseo_opengraph_image', 'alter_existing_opengraph_image' );
