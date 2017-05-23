---
layout: default
group:
subgroup: Architecture
title: Libraries
menu_title: Libraries
menu_order:
version: 2.0
github_link: architecture/arch_libraries.md
redirect_from: /guides/v1.0/architecture/arch_libraries.html
---

<!---
This topic is duplicated by:
architecture/archi_perspectives/components/arch_libraries.md,
which is currently published on DevDocs.

Thus, the {% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %} elements in this topic haven't been fixed.
-->

<h2 id="m2arch-libraries-overview">Overview</h2>
The Magento software can use the following types of libraries:

*	Magento {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} libraries, which are discussed in the next section.
*	Magento UI libraries, which are located in the <a href="{{ site.mage2000url }}lib/web" target="_blank">lib/web</a> directory.

	For more information, see <a href="{{ site.mage2000url }}lib/web/css/docs/source/README.md" target="_blank">library documentation on GitHub</a> and <a href="{{page.baseurl}}architecture/view/view-lib.html">View Library</a>.
*	Third-party libraries<!-- , which are located in the <a href="{{ site.mage2000url }}lib/internal" target="_blank">lib/internal</a> directory -->. These libraries include all PHP code (including the Zend libraries).

	Third-party libraries are organized by vendor to be PSR-0 compliant.

<h2 id="m2arch-libraries-mage">Magento PHP libraries</h2>
<a href="{{ site.mage2000url }}lib/internal/Magento/Framework" target="_blank">Magento PHP libraries</a> include code that is designed to be independent libraries of code useful to a Magento application. Each {% glossarytooltip 08968dbb-2eeb-45c7-ae95-ffca228a7575 %}library{% endglossarytooltip %} has minimal dependencies on any other library.

For example:

*	<a href="{{ site.mage2000url }}lib/internal/Magento/Framework/Filesystem" target="_blank">Magento\Framework\Filesystem</a> has PHP libraries for file system operations such as read, write, directory listing, and so on. We provide drivers for <a href="{{ site.mage2000url }}lib/internal/Magento/Framework/Filesystem/Driver/File.php" target="_blank">file</a>, <a href="{{ site.mage2000url }}lib/internal/Magento/Framework/Filesystem/Driver/Http.php" target="_blank">HTTP</a>, <a href="{{ site.mage2000url }}lib/internal/Magento/Framework/Filesystem/Driver/Https.php" target="_blank">HTTPS</a>, and <a href="{{ site.mage2000url }}lib/internal/Magento/Framework/Filesystem/Driver/Zlib.php" target="_blank">Zlib</a>.
*	<a href="{{ site.mage2000url }}lib/internal/Magento/Framework/App" target="_blank">Magento\Framework\App</a> is a special PHP library that is aware of Magento as an application. It represents a greater level of abstraction and provides the following:

	* <a href="{{page.baseurl}}architecture/modules/mod_and_areas.html">Application areas</a>
	* <a href="{{page.baseurl}}extension-dev-guide/routing.html">Routing requests</a>
	* Application state

<div class="bs-callout bs-callout-info" id="info">
  <p>Other Magento libraries do not reference <code>Magento\Framework\App</code>.</p>
</div>

<h2 id="m2arch-related">Related topics</h2>

* <a href="{{page.baseurl}}architecture/arch_asmodsys.html">Magento as a modular system</a>
* <a href="{{page.baseurl}}architecture/modules/mod_intro.html">Modules</a>
* <a href="{{page.baseurl}}architecture/arch_themes.html">Themes</a>
* <a href="{{page.baseurl}}architecture/arch_translations.html">Language packages</a>
