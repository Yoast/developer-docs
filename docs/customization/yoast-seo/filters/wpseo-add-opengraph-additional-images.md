---
id: wpseo-add-opengraph-additional-images
title: Yoast SEO - Allows to add an additional image to the end of the og:image tags array
sidebar_label: Add an additional image to the end of the og:image tags array
custom_edit_url: https://github.com/Yoast/developer-docs/edit/master/docs/customization/yoast-seo/filters/wpseo-add-opengraph-additional-images.md
---
The `wpseo_add_opengraph_additional_images` filter allows to add an additional image to the end of the og:image tags array. Each image added through the filter will have `og:image`, `og:image:width` and `og:image:height` tags.

## Usage

### Add an additional image to the end of the og:image tags array
```php
<?php
/**
 * Add an additional image to the end of the og:image tags array
 */
function add_additional_image_to_opengraph_tags( $image_container ) {
    $image_id = $some_id;
    $image_container->add_image_by_id( $image_id );
}
add_filter( 'wpseo_add_opengraph_additional_images', 'add_additional_image_to_opengraph_tags' );
```
