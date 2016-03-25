# Drupal 8 CMI

Separating config from content & being able to export config in code has always been a concern with Drupal. Solution to this started with the invent of features back in the days of Drupal 7 and has now become an integral part of Drupal 8.

Drupal 8 allows us to export configuration as YAML files. These can later be imported into another Drupal 8 instance with an easy to use interface. The  first step to get started with CMI is to enable the **Configuration Manager** module that bundles with Drupal 8 core.

![](Screen Shot 2016-03-25 at 11.56.15 PM.png)

The CMI interface gives us following 2 options for exporting the configuration:
* Exporting YAML files per component
* Exporting a config tarball of all the components


