UPGRADE 2.0
===========

## 2.0.0

### SonataAdminBundle

Now supporting the 3.0 version of the bundles

### CMSPageBundle

Please read the corresponding instructions [here](https://github.com/Th3Mouk/CMSPageBundle/blob/master/UPGRADE-2.0.md).

### Upgrade this bundle from 1.x

Add in your `AppKernel.php` :

```php
new Sonata\ClassificationBundle\SonataClassificationBundle(),
```

Then in your terminal launch `app/console sonata:easy-extends:generate SonataClassificationBundle --dest=src` command.

And again in the `AppKernel.php` :

```php
new Application\Sonata\ClassificationBundle\ApplicationSonataClassificationBundle(),
```
