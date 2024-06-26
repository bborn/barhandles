# README

[![npm version](https://badge.fury.io/js/barhandles.svg)](http://badge.fury.io/js/barhandles)
[![Build Status](https://travis-ci.org/bborn/barhandles.svg?branch=master)](https://travis-ci.org/bborn/barhandles)

Extract variable references from Handlebars templates.

### One Minute Overview

```javascript
import barhandles from "barhandles-ts";

barhandles.extract("{{foo.bar}}", callback);
// Callback will be invoked with ['foo', 'bar'], false

barhandles.extract("{{#with foo}}{{bar}}{{/with}}", callback);
// Callback will be invoked with ['foo', 'bar'], false

barhandles.extract("{{#each foo}}{{bar}}{{/each}}", callback);
// Callback will be invoked with ['foo', '#', 'bar'], false

barhandles.extract("{{#with foo}}{{#each bar}}{{../baz}}{{/each}}{{/with}}", callback);
// Callback will be invoked with ['foo','baz'], false
```

The second parameter passed to the callback is only present in version 0.4.0 and upwards. It indicates if the field
is considered to be optional. Barhandles by default assumes everything is required. Only in case of conditional sections
such as when using `{{#if}}…{{/if}}` it will mark attributs to be optional.

Barhandles also allows you to generate a hierarchical schema from your object model.

```javascript
barhandlers.extractSchema("{{foo.bar}}");
```

will produce:

```json
{
    "foo": {
        "_type": "object",
        "_optional": false,
        "bar": {
            "_type": "any",
            "_optional": false
        }
    }
}
```

### Change log

-   `v0.7.0`: Add support for subexpressions, migrate to Typescript
-   `v0.4.3`: Bug fixes
-   `v0.4.1`: Add support for adding behaviour of other directives
-   `v0.4.0`: Support for `{{#if}}` and optionals.
-   `v0.3.0`: Support for extracting a schema.
-   `v0.2.0`: Initial version
