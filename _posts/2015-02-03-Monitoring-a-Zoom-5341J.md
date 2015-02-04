---
layout: post
title: Monitoring a Zoom 5341J
---

I've been having issues with stability with my cable internet connection at home.  It seemed as though when it got colder, the connection would be more flaky - especially when I really wanted to finish my Dr. Who Netflix binge.

The cable modem's status page gives some pretty detailed statistics about the current connection status and various signal strengths.  Unfortunately, this is only a snapshot, which doesn't provide much value when you want to find coorelations in this data.

Which brought me to the idea of scraping the modem status page periodically with a Python script.  I was inspired (by this post)[http://www.perlmonks.org/bare/?node_id=600568] to write my own script to parse the modem status page and log it.

{% gist 8c6477f7630f944fb675 scrape-zoom.py %}

The script is simple and outputs a CSV file with all the modem stats contained on the page.  I've had this running for several weeks now without issue.  This will definitely help me pin down the root cause of my connection issues.
