Installation
============

Step 1: Download the Bundle
---------------------------
Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```console
$ composer require carizy/geolocation-bundle
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter](https://getcomposer.org/doc/00-intro.md)
of the Composer documentation.

You also need to have the repository inside your global composer.json:

```json
{
  "repositories" : [
      {
          "type": "git",
          "url": "https://github.com/Carizy/GeolocationBundle.git"
      } 
  ]
}
```
Of course you also need to be able to clone this bundle in ssh, check your rights.

Step 2: Enable the Bundle
-------------------------

Then, enable the bundle by adding it to the list of registered bundles
in the `app/AppKernel.php` file of your project:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // ...

            new Carizy\GeolocationBundle\GeolocationBundle(),
        );

        // ...
    }

    // ...
}

Step 3
