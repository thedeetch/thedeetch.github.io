---
layout: post
title: Creating Custom Hue Applications
---

**tl;dr** Creating a custom Hue app is fun and easy.

We use [Hue](http://gethue.com/) a lot where I work and recently I created a metadata aggregation tool with a [Solr](http://lucene.apache.org/solr/) backend and a simple [Handlebars](http://handlebarsjs.com/) frontend.  Originally, I demoed this as a standalone application, but I got to thinking - the users of the metadata will be mainly using Hue, so why not put this app there too?

Luckily, Hue has decent [SDK documentation](http://cloudera.github.io/hue/docs-3.7.0/sdk/sdk.html) that steps you through creating a custom Hue app.  One command gets you a blank project to work from.

```
$ ./build/env/bin/hue create_desktop_app metabase
```

Hue is a Django application, so being familiar with that, or at least Python, is a plus.

And once you're ready to deploy, a second command registers it with Hue.

```
$ ./build/env/bin/python tools/app_reg/app_reg.py --install metabase --relative-paths
```

A couple odd things I haven't figured out yet:

* The link to the new app gets placed under an "Other Apps" menu in the Hue toolbar
* Some of the built-in app icons use FontAwesome icons instead of images.  Not sure how to set up a custom app to use those instead of images.

The SDK docs do a good job explaining what's included with Hue by default - like the outdated Bootstrap 2.0 - but it gives you everything you need to create your own app and make it look like it shipped with Hue.
