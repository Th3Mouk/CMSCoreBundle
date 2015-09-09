UPGRADE 1.2
===============

## 1.2.0

The goal is to stand alone this bundle and give a fast solution for person who have already been started theirs projects.

This version take all config files, allowing fast inclusion and overwritting.

The missing files can now be fast import : 

```
    # Sonata Core Bundles
    - { resource: sonata/sonata_block.yml }
    - { resource: sonata/sonata_seo.yml }

    # Sonata Feature Bundles
    - { resource: sonata/sonata_admin.yml }
    - { resource: sonata/sonata_page.yml }
    - { resource: sonata/sonata_media.yml }
```

with this include : `- { resource: @Th3MoukCMSCoreBundle/Resources/config/config_fast_install.yml }`

The easier way to personnalize this files is to copying this files in your application and add the previous config (file by file)

The starter project will continue to present all the files ready to use for a fast symfony deployement with common managing file.

This version concern to all symfony framework modification like Twig etc ...

To understand the working of configuration and avoid error during personnalisation i advise to read the `Resources/config` folder
