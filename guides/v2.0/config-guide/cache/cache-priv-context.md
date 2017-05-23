---
layout: default
group: config-guide
subgroup: 08_Caching
title: HTTP context
menu_title: HTTP context
menu_order: 20
menu_node: 
level3_menu_node: level3child
level3_subgroup: cache-priv
version: 2.0
github_link: config-guide/cache/cache-priv-context.md
---

Caching servers and proxies usually use a {% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %} as the caching identifier; however, Magento URLs are not unique *enough* to allow caching by URL only. (We can {% glossarytooltip 0bc9c8bc-de1a-4a06-9c99-a89a29c30645 %}cache{% endglossarytooltip %} the customer group, selected language, whether the customer logged in or not, and so on).

To make each cached URL totally unique, we use *HTTP context variables*. Context variables enable the Magento application to serve different content on the same URL based on customer group, selected language, whether customer logged in or not, and so on.

Context variables must not be specific to exactly one user, because variables are used in cache keys for public content. In other words, a context variable per user results in a separate copy of content cached on the server for each user.

Magento combines context variables in a string, generates the cache from that string, and sets it as the value of the `X-Magento-Vary` cookie. HTTP proxies can be configured to calculate a unique identifier for cache based on the cookie and URL. For example, [our sample Varnish 4 configuration]({{ site.mage2000url }}app/code/Magento/PageCache/etc/varnish4.vcl#L63-L68){:target="_blank"} uses the following: 

{% highlight xml %}
sub vcl_hash {
if (req.http.cookie ~ "X-Magento-Vary=") {
hash_data(regsub(req.http.cookie, "^.?X-Magento-Vary=([^;]+);.*$", "\1"));
}
... more ...
}
{% endhighlight %}

For an example of a context class, see [Magento/Framework/App/Http/Context]({{ site.mage2000url }}lib/internal/Magento/Framework/App/Http/Context.php){:target="_blank"}.

#### Next
[Cache invalidation and private content versioning]({{ page.baseurl }}config-guide/cache/cache-priv-inval.html)