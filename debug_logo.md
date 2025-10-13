---
layout: default
title: Debug Logo
nav_exclude: true
permalink: /debug-logo/
---

# Debug Logo

**Variables**
- `site.url` = `{{ site.url }}`
- `site.baseurl` = `{{ site.baseurl }}`
- `site.logo` = `{{ site.logo }}`

**Try rendering the image using different paths/filters**

1) Using `site.logo` with `relative_url`  
`![]({{ "{{ site.logo | relative_url }}" }})`  
![]({{ site.logo | relative_url }})

2) Using absolute path from root: `![](/assets/logo.png)`  
![](/assets/logo.png)

3) Using `relative_url` filter:  
`![]({{ "'/assets/logo.png' | relative_url" }})`  
![]({{ '/assets/logo.png' | relative_url }})

4) Using `site.baseurl` explicitly:  
`![]({{ "'/assets/logo.png' | prepend: site.baseurl" }})`  
![]({{ '/assets/logo.png' | prepend: site.baseurl }})
