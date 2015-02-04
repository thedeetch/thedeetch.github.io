---
layout: post
title: Prettify YARN Web UI
---

Working with Hadoop at my day job is exciting.  There is a lot of velocity in the ecosystem and constant improvement in the tools we use.

[YARN](http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html) is a workload manager we use for our Hadoop clusters.  It does its job and does it well.

I do have a bunch of beefs...

Could the YARN web UI be prettier?  Or load faster?  I mean, yeah, they're using jQuery datatables, which is nice.  But could we not return the entire application history on the landing page?  Or use some coloring in the progress bars?  Or show times in local?  Or show elapsed times so I don't have to do math? Why show application stats for Dr. Who?

![YARN Web UI Ugly](/images/yarn-ui-ugly.png "YARN Web UI")

I know I'm being harsh, but this inspired me to write a tampermonkey/greasemonkey script to fit my needs.

{% gist 85e3d81ed4d80621fdd5 yarn-cluster-prettyfier.user.js %}

And now here is what it looks like:

![YARN Web UI Pretty](/images/yarn-ui-pretty.png "YARN Web UI Pretty!")

To install this script, click the "view raw" link on the bottom of the Gist.

I have more tweaks planned, like sorting by duration and limiting the number of returned applications.  So keep an eye on the Gist.
