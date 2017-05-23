---
layout: default
group: arch-guide
subgroup: Components
title: Language packages
menu_title: Language packages
menu_order: 9
version: 2.0
github_link: architecture/archi_perspectives/components/arch_translations.md
redirect_from: /guides/v1.0/architecture/components/arch_translations.html
---

## Overview {#m2arch-translations-overview}

Any text that is presented to the user can have several captions or labels on the control elements, notifications, and error messages. By default, Magento renders all these phrases in English (`US`) language (`en_US`). But if you deploy a {% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}storefront{% endglossarytooltip %} in a different language (or use the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento Admin{% endglossarytooltip %} panel in a different language), you can incorporate other dictionaries for translations.

You can use the language packages provided with Magento, create your own, or obtain packages from the community. Check out the language packages, modules, and themes available on Magento Marketplace.

Creating a {% glossarytooltip 9c4c7b9b-43f0-4454-8e8c-fb62ad40c35f %}language package{% endglossarytooltip %} is part of the process of *localizing* your storefront.

## Magento language packages

A <i>language package</i> is a collection of translation dictionaries for a particular language together with additional information that tells Magento how to process the information, including:

* `.csv` file contains the actual strings that comprise the language dictionary. A translation dictionary is a comma-separated value (`.csv`) file with at least two columns: the original phrase in the `en_US` {% glossarytooltip 05099dbb-d491-4e33-a065-16035cb2d4d9 %}locale{% endglossarytooltip %} and a translation of that phrase to another locale.

* `composer.json` file contains any dependencies for the language package and a mapping to its defined locale.

* `language.xml` file, where you declare a language package and establish any inheritance rules, if you are installing multiple language packages.

## About localization and internationalization

<i>Localization</i>  is the process of adapting a product or service to a particular language, culture, and preferred local display characteristics.  Ideally, a product or service is developed so that localization is relatively easy to implement.  For example, you might design technical illustrations for manuals in which the text can easily be changed to another language.

The process of structuring an application to support localization is termed <i>internationalization</i>. An internationalized product or service is easier to localize for a particular language than a product that has not been internationalized. The process of first enabling a product to be localized and then localizing it for different national audiences is also known as <i>globalization</i>.

For an overview of Magento translation-related issues, see <a href="{{page.baseurl}}frontend-dev-guide/translations/xlate.html">Translations overview</a>.

Procedures for creating language packages and dictionaries are described in <a href="{{page.baseurl}}config-guide/cli/config-cli-subcommands-i18n.html#config-cli-subcommands-xlate-dict-trans">Translation dictionaries and language packages</a>.

## Related topics {#m2arch-related}

<a href="{{page.baseurl}}architecture/archi_perspectives/components/modules/mod_intro.html">Modules</a>

<a href="{{page.baseurl}}architecture/archi_perspectives/components/arch_libraries.html">Libraries</a>

<a href="{{page.baseurl}}architecture/archi_perspectives/components/arch_themes.html">Themes</a>
