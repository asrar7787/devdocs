---
layout: default
group: mrg
subgroup: Enterprise Edition
title: Magento_GiftWrappingStaging module
menu_title: GiftWrappingStaging
menu_order: 2
version: 2.1
github_link: mrg/ee/GiftWrappingStaging.md
---

![Magento EE logo]({{site.baseurl}}common/images/ee-only_large.png)

## Overview

The Magento_GiftWrappingStaging {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}module{% endglossarytooltip %} is a part of the staging functionality in Magento EE. It allows to stage value of 'Allow Gift Wrapping' flag and price of the wrapping for each product update.

## Implementation details

The Magento_GiftWrappingStaging module adds to the Schedule Update form of a product the following functionality:

- Enable/disable gift wrapping ("Allow Gift Wrapping" field)
- Set a price for the gift wrapping ("Price for Gift Wrapping" field).

## Dependencies

You can find the list of modules that have dependencies on the Magento_GiftWrappingStaging module in the `require` section of the `composer.json` file. The file is located in the root directory of the module.

## Extension points

[The Magento dependency injection mechanism](http://devdocs.magento.com/guides/v2.1/extension-dev-guide/depend-inj.html) enables you to override the functionality of the Magento_GiftWrappingStaging module.

## Additional information

You can track [backward incompatible changes made in a Magento EE mainline after the Magento 2.0 release](http://devdocs.magento.com/guides/v2.0/release-notes/changes/ee_changes.html).
