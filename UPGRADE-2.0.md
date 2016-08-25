UPGRADE 2.0
===========

## 2.0.0

### Symfony

Drop the Symfony 2.3 support due to vich/uploader-bundle

### SonataAdminBundle

Now supporting the 3.0 version of the bundles

### CMSPageBundle

Please read the corresponding instructions [here](https://github.com/Th3Mouk/CMSPageBundle/blob/master/UPGRADE-2.0.md).

### Upgrade this bundle from 1.x

Add in your `AppKernel.php` :

```php
new Sonata\ClassificationBundle\SonataClassificationBundle(),
new FOS\JsRoutingBundle\FOSJsRoutingBundle(),
```

Then in your terminal launch `app/console sonata:easy-extends:generate SonataClassificationBundle --dest=src` command.

And again in the `AppKernel.php` :

```php
new Application\Sonata\ClassificationBundle\ApplicationSonataClassificationBundle(),
```

You need to upgrade `routing.yml` too by adding :

```yml
fos_js_routing:
    resource: "@FOSJsRoutingBundle/Resources/config/routing/routing.xml"
```
