---
layout: default
group: cloud
subgroup: 080_setup
title: Step 2, Install the CLI
menu_title: Step 2, Install the CLI
menu_order: 54
menu_node: 
level3_menu_node: level3child
level3_subgroup: workspace
version: 2.0
github_link: cloud/before/before-workspace-cli.md
---

## Install the command-line interface (CLI) {#cloud-ssh-cli-cli-install}
The Magento Enterprise Cloud Edition command-line interface (CLI) helps you manage your projects on Magento Enterprise Cloud Edition. 

To install the Magento Enterprise Cloud Edition CLI:

1.	Log in to your local development machine, or switch to, the [Magento file system owner]({{ page.baseurl }}cloud/before/before-workspace-file-sys-owner.html).
2.	Change to a directory to which the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento file system owner{% endglossarytooltip %} has write access (for example, the web server docroot).
1.	Enter the following command:

		curl -sS https://accounts.magento.cloud/cli/installer | php
2.	After the CLI downloads, an operating system-specific command displays.

	For example, on Ubuntu and CentOS, the command is similar to:

	<pre class="no-copy">source /home/magento_user/.bashrc</pre>

	For more information about the user shell profile, see [.bash_profile vs .bashrc](http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html){:target="_blank"}

	You can also add the `<magento user home dir>/.magento-cloud/bin` to the Magento user's `PATH`. 	If the user name is `magento_user`, the command is similar to the following:
	
		export PATH=$PATH:/home/magento_user/.magento-cloud/bin

	Consult operating system documentation for details.
		
4.	Verify the `magento-cloud` command is in your path by entering the following command:

		magento-cloud list

#### Next step
[Step 3, Enable Secure Shell (SSH)]({{ page.baseurl }}cloud/before/before-workspace-ssh.html)
