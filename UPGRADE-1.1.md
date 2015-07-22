UPGRADE 1.1
===============

## 1.1.0

### __Id4vMenuBundle 2.0.0__

Full integration of [KnpMenuBundle](https://github.com/KnpLabs/KnpMenuBundle)

BC Break with the old menu running

Replace the twig extension:
```twig
{{ render_menu("menu-principal", {template: "AppBundle:Menu:menu_mobile.html.twig"}) }}
```
By :
```twig
{{ knp_menu_render('app.vichy.menu.header', {template: "AppBundle:Menu:menu_mobile.html.twig"}) }}
``` 

The complete documentation to create a menu is available here: [KnpMenuBundle doc](http://symfony.com/doc/master/bundles/KnpMenuBundle/index.html), and here [Id4vMenuBundle](https://github.com/Id4v/MenuBundle)

## 1.1.1

### __SonataFormatterBundle__

Dependencies was re-added due to controllers and routing usefull for the link between Ckeditor and SonataMedia.
[CoopTilleulsCKEditorSonataMediaBundle](https://github.com/coopTilleuls/CoopTilleulsCKEditorSonataMediaBundle) can't remplace it because he extends SonataMediaBundle, and we can't easy extends entities.