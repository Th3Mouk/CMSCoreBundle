Installation
============

The installation is fast as thunder, follow my STEPS !
  
## Parameters

Add in your `parameters.yml.dist`

```
title_project:     CMS Starter
logo_project:      bundles/sonataadmin/logo_title.png

pixlr_secret:      TheSuperSecretHash
```

Name your title project and if you have a logo for your admin checkout the path.

## Composer 

`php composer.phar require th3mouk/cms-core-bundle ^1.2.0`

## Config

When composer is over, follow carefully configurations part of your application.

Add in your `config.yml`

```
# Sonata CMS Include Default Conf
- { resource: @Th3MoukCMSCoreBundle/Resources/config/config.yml }
- { resource: @Th3MoukCMSCoreBundle/Resources/config/bundles/ivory_ckeditor.yml }
- { resource: @Th3MoukCMSCoreBundle/Resources/config/config_fast_install.yml }
```

## AppKernel

Add all of them :

```
// Sonata Core
new Sonata\CoreBundle\SonataCoreBundle(),
new Sonata\AdminBundle\SonataAdminBundle(),
new Sonata\DoctrineORMAdminBundle\SonataDoctrineORMAdminBundle(),
new Sonata\BlockBundle\SonataBlockBundle(),
new Application\Sonata\BlockBundle\ApplicationSonataBlockBundle(),
new Sonata\IntlBundle\SonataIntlBundle(),
new Sonata\SeoBundle\SonataSeoBundle(),
new Sonata\CacheBundle\SonataCacheBundle(),
new Sonata\NotificationBundle\SonataNotificationBundle(),
new Application\Sonata\NotificationBundle\ApplicationSonataNotificationBundle(),
new Sonata\EasyExtendsBundle\SonataEasyExtendsBundle(),
new Knp\Bundle\MenuBundle\KnpMenuBundle(),

// CMF Integration
new Symfony\Cmf\Bundle\RoutingBundle\CmfRoutingBundle(),

// Sonata User
new FOS\UserBundle\FOSUserBundle(),
new Sonata\UserBundle\SonataUserBundle('FOSUserBundle'),
new Application\Sonata\UserBundle\ApplicationSonataUserBundle(),

// Sonata Page
new Sonata\PageBundle\SonataPageBundle(),

// Sonata Formatter
new Knp\Bundle\MarkdownBundle\KnpMarkdownBundle(),
new Sonata\FormatterBundle\SonataFormatterBundle(),

// CKEditor
new Ivory\CKEditorBundle\IvoryCKEditorBundle(),

// Sonata Media
new Sonata\MediaBundle\SonataMediaBundle(),
new Application\Sonata\MediaBundle\ApplicationSonataMediaBundle(),
new JMS\SerializerBundle\JMSSerializerBundle(),
new Liip\ImagineBundle\LiipImagineBundle(),

// Fixtures
new Doctrine\Bundle\FixturesBundle\DoctrineFixturesBundle(),
new Bazinga\Bundle\FakerBundle\BazingaFakerBundle(),

// Doctrine Extension
new Stof\DoctrineExtensionsBundle\StofDoctrineExtensionsBundle(),

// Uploads
new \Vich\UploaderBundle\VichUploaderBundle(),

// API
new FOS\RestBundle\FOSRestBundle(),
new Nelmio\ApiDocBundle\NelmioApiDocBundle(),

// Menu
new Id4v\Bundle\MenuBundle\Id4vMenuBundle(),

// CMS Starter
new Th3Mouk\CMSCoreBundle\Th3MoukCMSCoreBundle(),
new Th3Mouk\CMSPageBundle\Th3MoukCMSPageBundle(),
new Application\Th3Mouk\CMSPageBundle\ApplicationTh3MoukCMSPageBundle(),
```

If u don't know the utility of each of them I advise to read the corresponding doc at least the goal and usage part.

## Routing

Modify `routing.yml` add this at the end of the file

```
th3_mouk_cms_page:
    resource: "@Th3MoukCMSPageBundle/Resources/config/routing.yml"
    prefix:   /

th3_mouk_cms_core:
    resource: "@Th3MoukCMSCoreBundle/Resources/config/routing.yml"
    prefix:   /

gallery:
    resource: '@SonataMediaBundle/Resources/config/routing/gallery.xml'
    prefix: /media/gallery

media:
    resource: '@SonataMediaBundle/Resources/config/routing/media.xml'
    prefix: /media

sonata_cache_cache:
    resource: '@SonataCacheBundle/Resources/config/routing/cache.xml'
    prefix: /

sonata_page_exceptions:
    resource: '@SonataPageBundle/Resources/config/routing/exceptions.xml'
    prefix: /

sonata_page_cache:
    resource: '@SonataPageBundle/Resources/config/routing/cache.xml'
    prefix: /

sonata_media_pixlr:
    resource: '@SonataMediaBundle/Resources/config/routing/pixlr.xml'
    prefix: /admin/media

liip_imagine:
    resource: "@LiipImagineBundle/Resources/config/routing.xml"

sonata_user_security:
    resource: "@SonataUserBundle/Resources/config/routing/sonata_security_1.xml"

sonata_user_resetting:
    resource: "@SonataUserBundle/Resources/config/routing/sonata_resetting_1.xml"
    prefix: /resetting

sonata_user_profile:
    resource: "@SonataUserBundle/Resources/config/routing/sonata_profile_1.xml"
    prefix: /profile

sonata_user_register:
    resource: "@SonataUserBundle/Resources/config/routing/sonata_registration_1.xml"
    prefix: /register

sonata_user_change_password:
    resource: "@SonataUserBundle/Resources/config/routing/sonata_change_password_1.xml"
    prefix: /profile

sonata_user:
    resource: '@SonataUserBundle/Resources/config/routing/admin_security.xml'
    prefix: /admin

admin:
    resource: '@SonataAdminBundle/Resources/config/routing/sonata_admin.xml'
    prefix: /admin

sonata_admin:
    resource: .
    type: sonata_admin
    prefix: /admin
```

## Security

This is an example of the basic configuration, ADAPT IT ON YOUR N£€D !

`security.yml`
```
# you can read more about security in the related section of the documentation
# http://symfony.com/doc/current/book/security.html
security:
    # http://symfony.com/doc/current/book/security.html#encoding-the-user-s-password
    encoders:
        Application\Sonata\UserBundle\Entity\User : sha512
#        Symfony\Component\Security\Core\User\User: plaintext

    # http://symfony.com/doc/current/book/security.html#hierarchical-roles
    role_hierarchy:
        ROLE_ADMIN:       [ROLE_USER, ROLE_SONATA_ADMIN]
        ROLE_SUPER_ADMIN: [ROLE_ADMIN, ROLE_ALLOWED_TO_SWITCH]
        SONATA:
            - ROLE_SONATA_PAGE_ADMIN_PAGE_EDIT # if you are not using acl then this line must be uncommented
            - ROLE_SONATA_PAGE_ADMIN_BLOCK_EDIT

    access_decision_manager:
        strategy: unanimous

    # http://symfony.com/doc/current/book/security.html#where-do-users-come-from-user-providers
    providers:
        fos_userbundle:
            id: fos_user.user_provider.username_email

    # the main part of the security, where you can set up firewalls
    # for specific sections of your app
    firewalls:
        # disables authentication for assets and the profiler, adapt it according to your needs
        dev:
            pattern:  ^/(_(profiler|wdt)|css|images|js)/
            security: false

        admin:
            pattern:            /admin(.*)
            context:            user
            form_login:
                provider:       fos_userbundle
                login_path:     /admin/login
                use_forward:    false
                always_use_default_target_path: true
                check_path:     /admin/login_check
                failure_path:   null
                default_target_path:   /admin/dashboard
            logout:
                path:           /admin/logout
            anonymous:          true
            switch_user: true

        main:
            pattern:             .*
            context:             user
            form_login:
                provider:       fos_userbundle
                login_path:     /login
                use_forward:    false
                check_path:     /login_check
                failure_path:   null
            logout:             true
            anonymous:          true
            switch_user: true

    # with these settings you can restrict or allow access for different parts
    # of your application based on roles, ip, host or methods
    # http://symfony.com/doc/current/book/security.html#security-book-access-control-matching-options
    access_control:
        # URL of FOSUserBundle which need to be available to anonymous users
        - { path: ^/login$, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/register, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/resetting, role: IS_AUTHENTICATED_ANONYMOUSLY }

        # Admin login page needs to be access without credential
        - { path: ^/admin/login$, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin/logout$, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin/login_check$, role: IS_AUTHENTICATED_ANONYMOUSLY }

        # Secured part of the site
        # This config requires being logged for the whole site and having the admin role for the admin part.
        # Change these rules to adapt them to your needs
        - { path: ^/admin/, role: [ROLE_ADMIN, ROLE_SONATA_ADMIN] }
        - { path: ^/.*, role: IS_AUTHENTICATED_ANONYMOUSLY }
```

## Easy Extending of Bundle

This part is really important to make the website working and fully customizable.

The aim is to provide the application entities that will be used to operate the bundles.

We can access more details [here](https://sonata-project.org/bundles/easy-extends/master/doc/reference/introduction.html).

Launch this set of commands : 
```
php app/console sonata:easy-extends:generate SonataBlockBundle --dest=src
php app/console sonata:easy-extends:generate SonataMediaBundle --dest=src
php app/console sonata:easy-extends:generate SonataNotificationBundle --dest=src
php app/console sonata:easy-extends:generate SonataUserBundle --dest=src
php app/console sonata:easy-extends:generate Th3MoukCMSPageBundle --dest=src
```

## That's all folks !

Thanks for reading