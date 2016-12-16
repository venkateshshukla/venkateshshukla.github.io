---
published: true
title: Google Analytics with Github pages
layout: post
tags: [google]
---
Google analytics is a wonderful product by Google which helps us in tracking user interaction with your site.

Adding that to Github pages is an easy task, thanks to the amazing post [here](https://desiredpersona.com/google-analytics-jekyll/).

The best part about this blog post is that the local hosting is not tracked, owing to this section of `_includes/head.html`.

```javascript
{{"{% if jekyll.environment == 'production' "}}%}
{{"{% include analytics.html "}}%}
{{"{% endif "}}%}
```

Brief mention of the other parts.

`_config.yml`


```
# Google services
google_analytics: UA—XXXXXXXX-X
```

This property can be referred as `site.google_analytics` from anywhere in the project.

Finally, the analytics.html, referred to in the first section, add the google-analytics snippet with the tracking code placeholder.

An example here.


`_includes/analytics.html`


``` javascript
<script>
    (function(i, s, o, g, r, a, m) {
        i['GoogleAnalyticsObject'] = r;
        i[r] = i[r] || function() {
            (i[r].q = i[r].q || []).push(arguments)
        }, i[r].l = 1 * new Date();
        a = s.createElement(o),
            m = s.getElementsByTagName(o)[0];
        a.async = 1;
        a.src = g;
        m.parentNode.insertBefore(a, m)
    })(window, document, 'script', 'https://www.google-analytics.com/analytics.js', 'ga');

    ga('create', '{{"{{ site.google_analytics"}} }}', 'auto');
    ga('send', 'pageview');
</script>

```
