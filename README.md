# Drupal 8 CMI

Separating config from content & being able to export config in code has always been a concern with Drupal. Solution to this started with the invent of features back in the days of Drupal 7 and has now become an integral part of Drupal 8.

Drupal 8 allows us to export configuration as YAML files. These can later be imported into another Drupal 8 instance with an easy to use interface. In this article, we will be talkig about:
* How to import/export single configuration?
* How to perform a bulk export of all the configurations on a site?
* How to synchronize configuration in a dev > stage > prod workflow?
* Running Drupal 8 with the configuration on file rather than Database.

### Enabling the module:
The  first step to get started with CMI is to enable the **Configuration Manager** module that bundles with Drupal 8 core.

![](Screen Shot 2016-03-25 at 11.56.15 PM.png)

### Exporting/Importing Configuration:
The CMI interface gives us following 2 options for exporting the configuration:
* Exporting YAML files per component
* Exporting a config tarball of all the components

![](export_multiple_single.gif)

### How to synchronize configuration in a dev > stage > prod workflow?
**P.S.** To move configuration across instances, its necessary for the components to have the same UUID. Dev/Stage/Prod instances need to be clones of each other. 

 *CMI is not built for synchronizing a component from qed42.com to example.com.*
![](uuid_yml.png)

To understand the process, lets assume we need to create an image style test it on dev & then push it across to both stage & prod. In a world without CMI, the process would be to create it on dev, test it & then recreate it again over the other instances(stage & prod). With CMI, the steps would be as follows:
* Create the sync directory to hold all the configurations.
```mkdir sites/defalult/files/sync```
* Configure the same under config_directories array in settings.php.
```
$config_directories = array(
    CONFIG_SYNC_DIRECTORY => __DIR__ . '/files/sync'
);
```
* Create the image style on dev instance & test it.(Lets say we created an image style to scale images to 100X200 & named it as 100 x 200)
* Browse to ```/admin/config/development/configuration/full/export``` & click on export button. This will download a tarball of all the configurations in the system.
![](config_export_full.png)
Alternatively, we can use drush config commands to do the same:
```drush cex```
![](drush_config_export_full.png)
* Extract the tarball exported into the ```sync``` directory created in 1st step. If using drush, only the updated or new configurations will be exported into sync directory automatically.
* Push the changes to version control system in use(GIT, SVN etc.).
* Pull the changes on staging server. If the configuration is exported for the first time, there will be a lot of configuration files getting pulled in, else it will be only the updated or new configurations.
* Browse to ```admin/config/development/configuration```. An error message is displayed in case the UUIDs don't match.
![](config_sync_error.png)
Otherwise, 