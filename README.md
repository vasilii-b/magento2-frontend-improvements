# Magento 2 Frontend Improvements

This repository provides some hacks to improve the Magento 2 storefront performance.

## Compile styles for enabled modules only

#### Problem

By default, all the `_module.less` and `_widgets.less` files within the theme and from its parent are compiled in the `styles-m.css` and `styles-l.css`.

This should not happen when the module is disabled or even not installed on the store. To fix this, a patch has been created.

#### Solution

Follow [these instructions](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/composer.html) on how to apply patches via composer on Magento.

In the project's `composer.json` file add the following:

```json

  "extra": {
        "magento-force": "override",
        "composer-exit-on-patch-failure": true,
        "patches": {
            "magento/framework": {
                "Compile styles for enabled modules only": "https://raw.githubusercontent.com/vasilii-b/magento2-frontend-improvements/master/patches/composer/magento-framework/import-styles-for-enabled-modules-only.patch"
            }
        }
    }
```

In your terminal (project root) run `composer update`.

In case you don't get a message that patch applied, run `rm -rf vendor/magento/framework` then `composer update`.

### Compatibility

This solution works Magento 2.3.0 and above. Shouldn't work starting 2.5.0 because of this [PR](https://github.com/magento/magento2/pull/31593).
