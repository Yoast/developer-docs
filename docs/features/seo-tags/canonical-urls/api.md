---
id: api
title: Canonical URLs - API documentation
sidebar_label: API
custom_edit_url: https://github.com/Yoast/developer-docs/edit/master/docs/features/canonical-urls/api.md
description: Instructions on how to modify our canonical URL values programmatically.
---
import Alert from '../../../../../developer-site/src/components/Alert';

<Alert type="warning">

When integrating with Yoast SEO, please ensure you do not use any of the Yoast SEO classes in your own code until _after_ `plugins_loaded` has executed. This applies to both autoloading and non-autoloading solutions, such as Composer or when using `require()`. 
</Alert>

To change the canonical URL that Yoast SEO generated for a URL programmatically, you can use the `wpseo_canonical` filter.

## Change the canonical URL
For example, the following code would change the canonical on a page with ID `12345`:

```php
/**
 * Filter the canonical URL.
 *
 * @param string $canonical The current page's generated canonical URL.
 *
 * @return string The filtered canonical.
 */
function prefix_filter_canonical_example( $canonical ) {
  if ( is_page( 12345 ) ) {
    $canonical = 'https://example.com/canonical-url/';
  }

  return $canonical;
}

add_filter( 'wpseo_canonical', 'prefix_filter_canonical_example' );
```

## Remove the canonical URL
If you want to completely remove the canonical URL from a page, simply return false for that page, like so:

```php
/**
 * Filter the canonical URL.
 *
 * @param string $canonical The current page's generated canonical URL.
 *
 * @return bool|string The filtered canonical or false when we want to remove it.
 */
function prefix_filter_canonical_example( $canonical ) {
  if ( is_page( 12345 ) ) {
    return false;
  }

  return $canonical;
}

add_filter( 'wpseo_canonical', 'prefix_filter_canonical_example' );
```

Or to remove it from all pages, simply do:

```php
add_filter( 'wpseo_canonical', '__return_false' );
```
