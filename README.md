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
```

Step 3: Configuration of the Bundle
-------------------------

You need to add the following code inside yours app/config/routing.yml, app/config/config.yml, app/config/services.yml,
app/config/parameters.yml

```yaml
    \\routing.yml
    core:
        resource: "@CoreBundle/Resources/config/routing.yml"
        prefix:   /
```


```yaml
    \\config.yml
        assetic:
            bundles: [ 'CoreBundle']
            
        orm:
            dql:
                string_functions:
                    MD5: Carizy\CoreBundle\DQL\Md5
                    IF: Carizy\CoreBundle\DQL\IfElse
                datetime_functions:
                    DATEDIFF:  Carizy\CoreBundle\DQL\DateDiff
                    YEAR:  Carizy\CoreBundle\DQL\Year
                    MONTH: Carizy\CoreBundle\DQL\Month
                numeric_functions:
                    timestampdiff:  Oro\ORM\Query\AST\Functions\Numeric\TimestampDiff
            resolve_target_entities:
                CoreBundle\Entity\ACustomerProject: Carizy\CoreBundle\Entity\ACustomerProject
                
        simple_things_entity_audit:
            audited_entities:
                - Carizy\CoreBundle\Entity\CarAd
                - Carizy\CoreBundle\Entity\TechSummaryRdv
                - Carizy\CoreBundle\Entity\ExpertiseReport
       
        white_october_tcpdf:
            class: 'Carizy\CoreBundle\Services\SaleMandateGenerator\Model\Mandat'
```

```yaml
  \\services.yml
  
  autovista_saver:
          class: Carizy\CoreBundle\Classes\AutovistaSaver
          arguments: [ '@doctrine.orm.entity_manager' ]

  app.loan:
          class: Carizy\CoreBundle\Helper\Loan
          arguments: [ '@service_container' ]

  app.mail_jet_customer:
          class: Carizy\CoreBundle\Helper\MailJetCustomer
          arguments: [ '@service_container', '@doctrine.orm.entity_manager']

  app.mail_jet_pro:
          class: Carizy\CoreBundle\Helper\MailJetPro
          arguments: [ '@service_container', '@doctrine.orm.entity_manager']

  app.pipedrive_api:
      class: Carizy\CoreBundle\Helper\PipeDriveApiHelper
      arguments: [ '@service_container', '@doctrine.orm.entity_manager' ]

  app.message_bird_pro:
      class: Carizy\CoreBundle\Helper\MessageBirdPro
      arguments: [ '@service_container', '@doctrine.orm.entity_manager' ]

  app.message_bird_customer:
      class: Carizy\CoreBundle\Helper\MessageBirdCustomer
      arguments: [ '@service_container', '@doctrine.orm.entity_manager' ]

  app.working_days:
      class: Carizy\CoreBundle\Services\WorkingDayService
  
  imports:
      - { resource: '@CoreBundle/Resources/config/services.yml' }
```


```yaml
    \\parameters.yml
   scheduler_interval_hours : duration of a normla expertise
   feuvert_soap.event_duration :
   feuvert_soap.service_id
   feuvert_soap.estimated_time
   cdn_url
   expertise.photo.path
   carizy_api_token
    
```
