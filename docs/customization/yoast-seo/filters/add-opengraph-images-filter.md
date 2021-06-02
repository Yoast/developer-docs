---
id: add-opengraph-images-filter
title: Yoast SEO - Allows developers to add images to the OpenGraph tags
sidebar_label: Add images to the OpenGraph tags
custom_edit_url: https://github.com/Yoast/developer-docs/edit/master/docs/customization/yoast-seo/filters/add-opengraph-images-filter.md
---
Yoast SEO allows to filter the OpenGraph image that is set on WordPress posts, pages, archives pages, custom post type pages and their archives. This is done through the `wpseo_add_opengraph_images` filter. 

The filter receive an instance of an image container. The method [`add_image_by_id()`](https://github.com/Yoast/wordpress-seo/blob/5044f65f9801a7ef55b5ccec9738e086ca53f8cb/src/values/images.php#L56-L68) method can be used to add an image by its id.

In practise, the filter adds the image to the `og:image` if no image is set as featured image for the post. If an image is already set, the filter will replace it with the image which is passed to its callback function.



## Usage

### Filter the OpenGraph image for a WordPress page
```php
<?php
/**
 * Filter the OpenGraph image for a WordPress page
 */
function add_opengraph_image_to_page( $image_container ) {
	if ( is_page( $page_id ) ) {
		$image_id = $some_id;
		if ( $image_id ) {
            $image_container->add_image_by_id( $image_id );
		}
	}
}
add_filter( 'wpseo_add_opengraph_images', 'add_opengraph_image_to_page', 29 );
```

### Filter the OpenGraph image for WordPress archives pages
```php
<?php
/**
 * Filter the OpenGraph image for WordPress archives pages
 */
function add_opengraph_image_to_archives_pages( $image_container ) {
	if ( is_archive() ) {
		$image_id = $some_id;
		if ( $image_id ) {
            $image_container->add_image_by_id( $image_id );
		}
	}
}
add_filter( 'wpseo_add_opengraph_images', 'add_opengraph_image_to_archives_pages', 29 );
```
