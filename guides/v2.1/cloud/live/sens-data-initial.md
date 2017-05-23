---
layout: default
group: cloud
subgroup: Live
title: Example of managing system-specific settings 
menu_title: Example of managing system-specific settings
menu_order: 15
menu_node: 
level3_menu_node: level3child
level3_subgroup: sens-data
version: 2.1
github_link: cloud/live/sens-data-initial.md
---
 
This topic discusses how to manage default {% glossarytooltip 05099dbb-d491-4e33-a065-16035cb2d4d9 %}locale{% endglossarytooltip %} and static file optimization settings in your integration system. _Static file optimization_ means merging and minifying {% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %} and Cascading Style Sheets, and minifying {% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %} templates. Static file optimization should be disabled in integration (where you're testing) and enabled in staging and production.  

These particular settings are discussed only to explain how the procedure works; you can use the same procedure to manage any available settings. 

This example shows how to:

1.	Change the configuration in the integration server's {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %}.
2.	Create `config.local.php` and transfer it to your local system.
3.	Push `config.local.php` to the integration server
4.	Verify your settings are not editable in the Admin.
5.	Change settings again.
	1.	Delete `config.local.php` on the integration server.
	2.	Change configuration settings on the integration server.
	3.	Re-create and push the updated `config.local.php` to the integration server.

<!-- <div class="bs-callout bs-callout-info" id="info" markdown="1">
This example shows how you can set and lock configuration values for everything _except_ sensitive settings. You must set sensitive settings either as configuration variables or in the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento Admin{% endglossarytooltip %}. For more information, see [Sensitive configuration paths]({{ page.baseurl }}cloud/live/config-reference-sens.html).
</div> -->

## Required role
To complete the tasks discussed in this topic, you must have at minimum a project reader role with [environment administrator]({{ page.baseurl }}cloud/project/user-admin.html#loud-role-env) privileges.

## Configuration settings you can change {#cloud-clp-settings}
The following table shows the configuration settings affected by the `bin/magento magento-cloud:scd-dump` command. These are the configuration settings that you can manage in Git.

| Description  | Path in Magento Admin (omitting **Stores** > **Configuration**) | 
|--------------|--------------|----------------------|
| Store locale  | General > **General**, **Locale Options** > **Locale**  |  
| Static asset signing |  Advanced > **Developer**, **Static Files Settings** > **Static Files Signing** 
| Server-side or client-side LESS compilation  | Advanced > **Developer**, **Frontend Developer Workflow** > **Workflow type** 
|  HTML minification | Advanced > **Developer**, **Template Settings** > **Minify Html**  
| JavaScript minification  | Advanced > **Developer**, **JavaScript Settings** > (several options)   
| {% glossarytooltip 6c5cb4e9-9197-46f2-ba79-6147d9bfe66d %}CSS{% endglossarytooltip %} minification  | Advanced > **Developer**, **CSS Settings** > **Merge CSS Files** and **Minify CSS Files**
| Disable modules output |  Advanced > **Advanced** > **Disable Modules Output** |

## Prerequisite
Before you continue, make sure you review our [recommended procedure]({{ page.baseurl }}cloud/live/sens-data-over.html#cloud-config-specific-recomm) for managing the configuration.

{% collapsibleh2 Get started %}

### Step 1: Synchronize with master

To synchronize your local system with the `master` branch:

1.	On your local system, switch to the [Magento file system owner]({{ page.baseurl }}install-gde/prereq/file-sys-perms-over.html).
2.	Log in to your Magento Enterprise Cloud Edition project.

		magento-cloud login
3.	Switch to the project root directory.
4.	Find the current branch.

		git branch
4.	If necessary, [merge changes in the current]({{ page.baseurl }}cloud/howtos/environment-tutorial-env-merge.html) branch with the `master` branch.
5.	Switch to the master branch locally.

		magento-cloud environment:checkout master
6.	Pull updated code.

		git pull origin master
		
### Step 2: Find Admin login information {#cloud-deploy-admin-login}
To find login information for the integration server Admin:

1.	Log in to your local system as the Magento file system owner.
2.	Find the integration server URL and Admin login information:

		magento-cloud environment:url
		magento-cloud variable:list
3.	Using the preceding information, log in to the integration server's Admin.

{% endcollapsibleh2 %}

{% collapsibleh2 Step 1: Change the configuration in the integration server Admin %}

This section discusses how to change the locale for the Default Config and also how to change static file optimization settings in the integration server. You can change different settings if you wish; see [List of system-specific configuration settings]({{ page.baseurl }}cloud/live/sens-data-over.html#cloud-config-specific-list) for details.

To change locale and static file optimization settings:

1.	Log in to the integration server Admin with the information you found in [Step 2: Find Admin login information](#cloud-deploy-admin-login).
1.	Click **Stores** > Settings > **Configuration** > General > **General**. 
2.	In the right pane, expand **Locale Options**. 
3.	From the **Locale** list, change the locale. (You can change it back later.)

	The following figure shows an example.

	![Change the locale]({{ site.baseurl }}common/images/cloud_var_locale.png){:width="400px"}
4.	Click **Save Config**.
5.	In the left navigation pane, click **Advanced** > **Developer**.
5.	In the right pane, expand **Template Settings**.
6.	Clear the **Use default value** check box next to the **Minify Html** list.
7.	From the **Minify Html** list, click **No**.
5.	In the right pane, expand **CSS Settings**.
6.	From the **Merge CSS Files** list, click **No**.
7.	From the **Minify CSS Files** list, click **No**.

	The following figure shows an example.

	![Set static file optimization settings]({{ site.baseurl }}common/images/cloud_vars_set-minify.png){:width="550px"}
8.	Click **Save Config**.
9.	If prompted, [flush the Magento cache](http://docs.magento.com/m2/ee/user_guide/system/cache-management.html){:target="_blank"}.
10.	Log out of the Magento Admin.

{% endcollapsibleh2 %}

{% collapsibleh2 Step 2: Create config.local.php and transfer it to your local system %}
This section discusses how to create `config.local.php` on the integration server using a command you run on your local machine. 

This procedure corresponds to step B, 1&ndash;2 of our [recommended procedure]({{ page.baseurl }}cloud/live/sens-data-over.html#cloud-config-specific-recomm). After you create `config.local.php`, transfer it to your local system so you can add it to Git.

To create `config.local.php` on the integration server:

{% include cloud/sens-data-create-config-local.md %}

The following snippet from `config.local.php` show an example of changing the default locale to `en_GB` and changing static file optimization settings:

<pre class="no-copy">
 'general' =>
      array (
        'locale' =>
        array (
          'code' => 'en_GB',
          'timezone' => 'UTC',
        ),

        ... more ...

 'dev' =>
      'template' =>
        array (
          'allow_symlink' => '0',
          'minify_html' => '0',
        ),
        
        ... more ...

        'js' =>
        array (
          'merge_files' => '0',
          'enable_js_bundling' => '0',
          'minify_files' => '0',
        ),
        'css' =>
        array (
          'merge_css_files' => '0',
          'minify_files' => '0',
        ),
</pre>

{% endcollapsibleh2 %}

{% collapsibleh2 Step 3: Push config.local.php to the integration server %}
Now that you've created `config.local.php` and transferred it to your local system, commit it to Git and push it to your integration server. This procedure corresponds to step B, 3&mdash;4 of our [recommended procedure]({{ page.baseurl }}cloud/live/sens-data-over.html#cloud-config-specific-recomm).

	git add app/etc/config.local.php && git commit -m "Add system-specific configuration" && git push origin master

Wait for deployment to complete.

{% endcollapsibleh2 %}

<p id="cloud-set-verify"></p>{% collapsibleh2 Step 4: Verify your configuration changes %}
After you push `config.local.php` to your integration server, any values you changed should be unavailable in the Magento Admin.

In this example, the default locale and static file optimization settings should not be editable in the Admin.

To verify your configuration changes:

1.	If you haven't done so already, log out of the integration server's Magento Admin.
2.	Log back in to the Admin.

	You can find login information as discussed in [Step 2: Find Admin login information](#cloud-deploy-admin-login)
4.	Click **Stores** > Settings > **Configuration** > General > **General**.
5.	In the right pane, expand **Locale Options**.

	Notice several fields cannot be edited, as shown in the following sample.

	![Can't edit certain values in the Admin]({{ site.baseurl }}common/images/cloud_var_not-editable.png){:width="550px"}
6.	In the left navigation pane, click Advanced > **Developer**.
7.	In the right pane, expand **Template Settings**, **JavaScript Settings**, and **CSS Settings**. 

	Notice several fields cannot be edited, as shown in the following sample.

	![Can't edit certain values in the Admin ]({{ site.baseurl }}common/images/cloud_var_not-editable2.png){:width="550px"}
8.	Log out of the Magento Admin.

{% endcollapsibleh2 %}

{% collapsibleh2 Step 5: Change system-specific configuration settings %}
This section discusses how to change system-specific settings. Our [recommended procedure]({{ page.baseurl }}cloud/live/sens-data-over.html#cloud-config-specific-recomm) is to make the changes on the integration server and repeat the process of creating `config.local.php` and pushing it back to the integration server.

For this example, we'll use static file optimization settings. If you've already changed those settings, you can use this procedure to set other options of your choosing.

### Delete config.local.php on the integration server
Before you can change settings on the integration server, you should delete `app/etc/config.local.php` so all settings are available in the Admin. (Any non-default setting in `config.local.php` is uneditable in the Admin.)

To delete `config.local.php`:

1.	On your local system, make sure you're on the `master` branch.
2.	SSH to the integration server:

		magento-cloud ssh
3.	Delete `config.local.php`.

		rm app/etc/config.local.php
4.	Close the SSH tunnel.

		exit

### Change configuration values in the integration server Admin
To change values in the Admin:

1.	If you haven't done so already, log out of the Magento Admin.
1.	Log in to the integration server's Admin.

	You can find login information as discussed in [Step 2: Find Admin login information](#cloud-deploy-admin-login)
4.	Click **Stores** > Settings > **Configuration** > **Advanced** > **Developer**.
5.	In the right pane, expand **Template Settings**.
6.	Clear the **Use default value** check box next to the **Minify Html** list.
7.	From the **Minify Html** list, click **Yes**.
5.	In the right pane, expand **CSS Settings**.
6.	From the **Merge CSS Files** list, click **Yes**.
7.	From the **Minify CSS Files** list, click **Yes**.

	The following figure shows an example.

	![Set static file optimization settings]({{ site.baseurl }}common/images/cloud_vars_reset-minify.png){:width="550px"}
8.	Click **Save Config**.
9.	If prompted, [flush the Magento cache](http://docs.magento.com/m2/ee/user_guide/system/cache-management.html){:target="_blank"}.
10.	Log out of the Magento Admin.

### Add the changes to a new version of config.local.php
{% include cloud/sens-data-create-config-local.md %}

### Push the changes to Git
To push your changes, enter the following command:

	git add app/etc/config.local.php && git commit -m "Add system-specific configuration" && git push origin master

Wait for deployment to complete.

Optionally [verify the changes](#cloud-set-verify), and verify that the changes are not editable in the Admin.

{% endcollapsibleh2 %}





