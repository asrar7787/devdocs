---
layout: default
group: cloud
subgroup: 080_setup
title: Overview of a Magento workspace
menu_title: Overview of a Magento workspace
menu_order: 51
menu_node: 
level3_menu_node: level3child
level3_subgroup: workspace
version: 2.0
github_link: cloud/before/before-workspace.md
---

The following sections discuss your options for setting up a Magento Enterprise Cloud Edition project.

We assume you'll install the Magento software so you can use the command line and the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento Admin{% endglossarytooltip %} on your laptop. That means you must set up the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento file system owner{% endglossarytooltip %} on your laptop so files and directories you created are owned by that user.

To be able to manage your projects, environments, and services, you must set up the Magento Enterprise Cloud Edition command-line interface (CLI) and Secure Shell (SSH). These tools enable you to perform tasks like:

*	Work on a local branch
*	Branch and merge in your project
*	Push changes to the parent branch
*	Pull changes from the parent branch

This guide assumes you're working on a UNIX system or in a UNIX shell environment. On Windows, you can use a UNIX environment like Cygwin or you can use Putty. The tool you use is up to you.

#### Next step
[Step 1, Set up an account]({{ page.baseurl }}cloud/before/before-workspace-cloud-account.html)


