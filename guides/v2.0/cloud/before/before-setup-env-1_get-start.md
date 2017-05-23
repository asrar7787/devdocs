---
layout: default
group: cloud
subgroup: 080_setup
title: Step 1, Get started setting up an environment
menu_title: Step 1, Get started setting up an environment
menu_order: 161
menu_node: 
level3_menu_node: level3child
level3_subgroup: setupenv
version: 2.0
github_link: cloud/before/before-setup-env-1_get-started.md
redirect from: 
  -  /guides/v2.0/cloud/access-acct/set-up-env.html
  -  /guides/v2.1/cloud/access-acct/set-up-env.html
---

{::options syntax_highlighter="rouge" /}

The topics in this section discuss how to get started developing on Magento Enterprise Cloud Edition. All developers should perform the tasks discussed in these topics.

## Set up SSH {#setup-env-setup}
This is a one-time setup that was covered previously in this guide; skip this section if you've already enabled SSH.

{% include cloud/enable-ssh.md %}

## Set global Git variables
To set global Git variables:

To set global Git variables required to commit or push to an environment (that is, Git branch), enter the following commands:

	git config --global user.name "<your name>"
	git config --global user.email <your e-mail address>

For more information, see [First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup#_first_time){:target="_blank"}

#### Next step
[Step 2, Clone the project]({{ page.baseurl }}cloud/before/before-setup-env-2_clone.html)