### NOTE: This repo got deprecated. We split it into separate repos. Please see [hydrogen.module.core](https://github.com/magnetcoop/hydrogen.module.core), [hydrogen.module.session.cognito](https://github.com/magnetcoop/hydrogen.module.session.cognito) and [hydrogen.module.session.keycloak](https://github.com/magnetcoop/hydrogen.module.session.keycloak)

# hydrogen.module.cljs for Duct

It implements two modules for [Duct](https://github.com/duct-framework/duct).
`hydrogen.module.cljs.core` brings in config for doing SPAs and `hydrogen.module.cljs.session` further enriches it
 to support OIDC-based session management.

## Installation

[![Clojars Project](https://img.shields.io/clojars/v/hydrogen/module.cljs.svg)](https://clojars.org/hydrogen/module.cljs)

## Usage

For SPA:
```edn
{:hydrogen.module.cljs/core {}}
```

For SPA with session management:
```edn
{:hydrogen.module.cljs/core {}
 :hydrogen.module.cljs/session {}}
```

And a more realistic example:
```edn
{:hydrogen.module.cljs/core
  {:externs-paths {:production ["src/my-app/client/externs.js"
                                "src/my-app/client/google_maps_api_v3_36.js"]
                   :development ["oksol/client/google_maps_api_v3_36.js"]}}
  :hydrogen.module.cljs/session {}}
```

### Additional options

- **Externs**\[1\] - to configure them use `:externs-paths` option. It accepts two formats:
    - `{:externs-paths ["a.js" "b.js"]}` - this would apply both files as externs both in development environment
     (as part of `:duct.server/figwheel` config)
     and in production environment
     (as part of `:duct.compiler/cljs` config).
    - `{:externs-paths {:production ["a.js"] :development ["x.js" "y.js"]}}`
- This module is used by Hydrogen CE and by [Hydrogen duct template](https://github.com/magnetcoop/hydrogen.cljs.duct-template).
For this reason it usually starts with `:add-example-api? true` option to make running demo more effortless. The default for this option is `false` so there's probably nothing for you to care about :)
 
#### Note
Figwheel expects files with .js extension inside its source
directories to be a foreign library. And foreign libraries **MUST**
declare a namespace. In fact, figwheel assumes it, and if it
doesn't find it and can't map the file back to a source .cljs file,
it bombs out with a NullPointerException.

So even if this is *NOT* a foreign library, but just an externs file,
add a namespace declaration to prevent figwheel from crashing.

Like this: `goog.provide('google.maps');`

## License

Copyright (c) 2018, 2019 Magnet S Coop.

The source code for the library is subject to the terms of the Mozilla Public License, v. 2.0. If a copy of the MPL was not distributed with this file, You can obtain one at https://mozilla.org/MPL/2.0/.
