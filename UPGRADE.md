# Upgrade guide

## 0.12 (07.10.2017)

* Update composer.json so "modera/foundation" would point to "^2.56.0" version

## 0.11 (18.06.2017)

* Update composer.json so "modera/mjr" would point to "~0.5.0" version
* Update composer.json so "modera/theme" would point to "~0.2.0" version
* Update composer.json so "modera/foundation" would point to "^2.55.0" version
* [MPFE-993] Database connection credentials now are specified using environment variables, update your `app/config/parameters.yml`,
for a way how these can be defined refer to `whaler.yml` file.
* bugfix [MPFE-984] Run this query `ALTER TABLE modera_translations_translationtoken CONVERT TO CHARACTER SET utf8 COLLATE utf8_bin;` 
  in MySQL database, this will make `modera:translations:import` command work properly in cases when tokens characters' case has 
  been changed, by default MySQL considered "foo" and "FOO" column values to be identical, by converting the collation to utf8_bin we
  are telling MySQL to consider those to be different values.
* [MPFE-980] If you are using nginx configs provided in `.whaler` directory please update gzip section as 
illustrated in this [commit](https://github.com/modera/foundation-standard/commit/d521dd0701ec8784be075e00ef7778ade1707dd5), 
it will reduce amount of data transferred through the network for about 80%. Also it is recommended to enable optimistic 
cache by adding `location` block, see this [commit](https://github.com/modera/foundation-standard/commit/36b8068c477ed9b1e2ca826b7b3fb8aab5f6a412) 
for more details. Once updated do not forget to restart Nginx. Beware that you need to increase a version number in `/modera-version.txt` 
file whenever a new version of application is deployed (when production environment is used). See 
from `VersionResolving\StandardVersionResolver` MJRCacheAwareClassLoaderBundle for more details. If the version number is not
increased then browser will continue using ExtJS classes that could have been possibly cached once user opened a section.

## 0.10

* Update composer.json so "modera/mjr" would point to "~0.3.0" version
* Update composer.json so it would include [modera/foundation](https://github.com/modera/foundation) and exclude
 packages that modera/foundation "replaces" (see ["replace"](https://github.com/modera/foundation/blob/master/composer.json#L34) 
 section of modera/foundation package).
* Update `.whaler` directory so it would use latest configuration files. See 
[5a7b6b5 changeset](https://github.com/modera/foundation-standard/commit/0a20324cb480dc7b18f6727ea9779a75177ce388) for 
related changeset. Updated configuration files make it easier to install additional application to the platform (such as chat).

## 0.9

* Update your composer.json file so it would use modera/foundation fat-repo instead of directly specifying all nested
packages. See [composer.json changeset](https://github.com/modera/foundation-standard/commit/52db17a084bf1a0461e47a98dd7353178c4ccbc7#diff-b5d0ee8c97c7abd7e3fa29b9a27d1780) for more details.
One composer.json has been updated don't forget to run `composer update`.

## from 0.7 to 0.8

* Make sure that your composer.json includes "repositories" section
as well as two new dependencies - modera/mjr, modera/theme. For details see this 
[composer.json changeset](https://github.com/modera/foundation-standard/commit/298da9ff06848f4aca53b2e5926268ff40bacce0#diff-b5d0ee8c97c7abd7e3fa29b9a27d1780).
* Run `composer update`, it is very important that you would have a latest version of
[composer-symfony-web-asset-installer-plugin plugin](https://github.com/modera/composer-symfony-web-asset-installer-plugin). This
plugin is used to install "mjr" and "theme" to `web` directory.
* Delete `.mjr` directory

Related commits:
* [298da9ff06848f4aca53b2e5926268ff40bacce0](https://github.com/modera/foundation-standard/commit/298da9ff06848f4aca53b2e5926268ff40bacce0)