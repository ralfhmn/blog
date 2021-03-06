---
title: 'Symfony2 with Assetic: Automatically update assets_version on deploy'
author: Markus Tacker
excerpt: |
  If you're using <a href="http://symfony.com/doc/current/reference/configuration/framework.html#assets-version">assetic</a> to manage your assets in your Symfony2 project you have probably already wondered if there is a way to update the <code>assets_version</code> parameter automatically with every deploy.
layout: post
permalink: symfony2-with-assetic-automatically-update-assets_version-on-deploy
categories:
  - development
tags:
  - Symfony2
  - Snippets
---
If you&#8217;re using [assetic][1] to manage your assets in your Symfony2 project you have probably already wondered if there is a way to update the `assets_version` parameter automatically with every deploy.

On my boxes I use this little command to update the `assets_version` to the latest unix timestamp:

> ``V=`date +%s`; sed -i -r -e "s/(\W+)assets_version:(\W+)[^\n]+/\1assets_version:\2$V/" app/config/parameters.yml`` 

It searches the `parameters.yml` and updates the `assets_version` line with the current unix timestamp (e.g. `1380833873`). It also honors the current indentation used in the file which may vary in YAML.

This statement could be added to your `composer.json`&#8216;s `post-install-cmd` or `post-update-cmd` section or any other deploy script you are using.

After that just make sure to update your assets via

> `app/console assetic:dump`

 [1]: http://symfony.com/doc/current/reference/configuration/framework.html#assets-version
