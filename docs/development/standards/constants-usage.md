---
id: constants-usage
title: Standards - Constants usage
sidebar_label: Constants usage
custom_edit_url: https://github.com/Yoast/developer-docs/edit/master/docs/development/standards/constants-usage.md
---

## Constants usage

We want to keep the usage of constants throughout our code base organized and easy to understand. At the same time we want to ensure classes don't have unnecessary dependencies on one another. Therefore you should separate constants into their own class.

Wrapping constants in a class has the additional benefit of enabling autoloading. This also means you need no additional setup to load them whenever required.

All such wrapping classes should be added to the `src/constants` directory.

For example, such a wrapping class could look as follows:
```php
namespace Yoast\WP\SEO\Constants;

class Link_Types {
    /**
     * Internal links are links that direct to the same site and are not images.
     */
    const INTERNAL = 'internal';

    /* More constants here */
}
```

You could then use this class like this:
```php
use Yoast\WP\SEO\Constants\Link_Types;

if ( $link->type === Link_Types::INTERNAL ) {
    // Do something.
}
```

There is one exception to this rule. When adding a constant that is only used in a single class you should add it to that class. These constants should have a docblock marking them as @internal.

For example:
```php
class Example {

    /**
     * A clear and concise explanation of this constant.
     *
     * @internal
     */
    const INTERNAL_CONSTANT = 'This is not used anywhere else';

    /**
     * A clear and concise explantion of this function.
     *
     * @return string The return value.
     */
    public function get_thing() {
        return \get_option( self::INTERNAL_CONSTANT );
    }
}
```

We also considered two other alternatives:
1. Files including only namespaced constants without a wrapping class. However this would necessitate additional effort to load these files. Any usage would also lack the additional classname providing context to the constant's origins.
2. Constants inside the classes where they were most used. This would create additional dependencies between classes. Which in turn could make refactoring and future changes more difficult and prone to errors.
