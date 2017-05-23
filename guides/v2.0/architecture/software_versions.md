---
layout: default
group: arch-guide
subgroup: Architectural Basics
title: Magento 2.0 software versions
menu_title: Magento 2.0 software versions
menu_order: 3
version: 2.0
github_link: architecture/software_versions.md
level3_menu_node: level3child
level3_subgroup: versioning

redirect_from: /guides/v1.0/architecture/software_versions.html
---

## Overview

Magento versioning policy addresses the concerns of two main types of users:

* <i>merchants</i>, who are focused on **product version numbers**. This product version number loosely corresponds to a platform version.

* <i>extension developers</i>, who focus on **module version numbers**. Each  {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}module{% endglossarytooltip %} is released in its own {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} package, which is identified with a module version number.

## Product version numbers (merchant focus)

All merchant projects depend on the CE {% glossarytooltip 7490850a-0654-4ce1-83ff-d88c1d7d07fa %}metapackage{% endglossarytooltip %}. (A <i>metapackage</i> consists of a `.zip` file that contains more than one {% glossarytooltip b57038ca-7906-4fce-a00f-d614b81d5301 %}Composer package{% endglossarytooltip %}.) Projects can specify a dependency on a specific version number (such as 2.0.1) or use a pattern to pick up patches automatically (such as 2.0.*)

Products are currently restricted to Magento Community Edition (CE) and Magento Enterprise Edition (EE). The version numbers of editions are designed for use in discussions with merchants. That is, major and minor increments to the version number will reflect the significance of changes to merchants. This may or may not reflect equally significant changes to developers.

You can easily view the product version number of your Magento installation in the right footer of the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento Admin{% endglossarytooltip %} (for example, **Magento** ver. 2.0.0-rc).


## Software version numbers (extension developer focus)

Software version (module)  numbers are relevant only to developer-level discussions. {% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}Extension{% endglossarytooltip %} developers typically depend on module major version numbers using version patterns such as 100.*.

If an extension developer depends on a private API, he specifies the major and minor version number such as 100.0.* to prevent the extension from working with the next CE release. This versioning practice forces merchants to upgrade to a newer version of the extension when they upgrade the CE release level.

The Magento team changes the major version number when we make a change that will affect extension developers. Examples of such changes include public {% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %} changes and significant {% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}layout{% endglossarytooltip %} file changes.

## Schema and data version numbers (extension developer focus)

Schema and data version numbers are relevant only to developer-level discussions.  Magento uses these version numbers during the installation and upgrade process.

Some modules contain tables of data, and these tables are assigned a schema version number. Changes to the table structure must be reflected in this schema version number. (Table structure changes can include the addition or deletion of a column, for example.) Changes to table data are captured in the data version number.

For information on the types of schema changes that affect a module's schema version number, see section 2 of Introducing SchemaVer for semantic versioning of schemas.

If you are developing an extension, specify the schema version of each module in its `module.xml` file. Magento stores this schema version of each module within the read-only `setup_module` table of the Magento database.

If you are installing or upgrading Magento from the command line, you have the option to upgrade in stages: first upgrade only schemas of tables and then upgrade data. During the upgrade process, Magento tracks these version changes in the setup_module table by automatically updating from the version value in `etc/module.xml` file.

## Composer package version numbers

Each module is released as a Composer package, and Magento uses Composer to define dependencies and compatibility between packages. A software version number identifies the Composer package for each module. The Magento engineering team assigns these versioning numbers  based on semantic versioning. As a result, **a product version number will differ from software version number**. Product version number is reflected in the Composer package for the Product (meta-package) version numbers. Software version number is reflected in the Composer package for the module version numbers. For example, a change from CE 2.0 to 2.1 could be more significant from an engineering perspective, and perhaps trigger a major version number change at the Composer package version number level.

## Patches

Release versioning and semantic versioning work together. Patches change only the last digit, which allows 100.0.n style patterns to be used across patch levels. Backward-compatible changes to the public API and documented behavior of a module trigger a minor number change, allowing 100.* style patterns to be used when an extension uses only public APIs.

## Related topics

* <a href="{{page.baseurl}}architecture/back-compatibility.html">Backward compatibility</a>

* <a href="{{page.baseurl}}architecture/archi_perspectives/ABasics_intro.html">Architectural basics</a>
