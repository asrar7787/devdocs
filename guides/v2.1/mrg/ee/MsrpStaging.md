---
layout: default
group: mrg
subgroup: Enterprise Edition
title: Magento_MsrpStaging module
menu_title: MsrpStaging
menu_order: 2
version: 2.1
github_link: mrg/ee/MsrpStaging.md
---

![Magento EE logo]({{site.baseurl}}common/images/ee-only_large.png)

## Overview

The Magento_MsrpStaging {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}module{% endglossarytooltip %} is a part of the staging functionality in Magento EE. It enables you to stage the manufacturer's suggested retail price.

## Implementation details

The Magento_MsrpStaging module extends the Magento_Msrp module to be used in staging. It adds the following fields in the Advice Pricing form:

- Manufacturer's Suggested Retail Price
- Display Actual Price

## Dependencies

You can find the list of modules that have dependencies on the Magento_MsrpStaging module in the `require` section of the `composer.json` file. The file is located in the root directory of the module.

## Extension points

[The Magento dependency injection mechanism](http://devdocs.magento.com/guides/v2.1/extension-dev-guide/depend-inj.html) enables you to override the functionality of the Magento_MsrpStaging module.

## Additional information

For more Magento 2 developer documentation, see [Magento 2 Developer Documentation](http://devdocs.magento.com). Also, there you can track [backward incompatible changes made in a Magento EE mainline after the Magento 2.0 release](http://devdocs.magento.com/guides/v2.0/release-notes/changes/ee_changes.html).
