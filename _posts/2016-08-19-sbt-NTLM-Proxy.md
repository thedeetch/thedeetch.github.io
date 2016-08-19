---
layout: post
title: sbt NTLM Proxy
---

I've found that using [sbt](http://www.scala-sbt.org/) behind an NTLM proxy at work doesn't quite work as advertised.  According to [the documentation](http://www.scala-sbt.org/0.13/docs/Setup-Notes.html#HTTP%2FHTTPS%2FFTP+Proxy), all you need to set is 

```
-Dhttp.proxyHost=myproxy -Dhttp.proxyPort=8080 -Dhttp.proxyUser=username -Dhttp.proxyPassword=mypassword
```

But I've found that I get this error buried in the stack trace in the sbt logs.

```
Caused by: java.lang.NullPointerException
        at com.sun.security.ntlm.Client.type3(Client.java:161)
        at sun.net.www.protocol.http.ntlm.NTLMAuthentication.buildType3Msg(NTLMAuthentication.java:241)
        at sun.net.www.protocol.http.ntlm.NTLMAuthentication.setHeaders(NTLMAuthentication.java:216)
        at sun.net.www.protocol.http.HttpURLConnection.getInputStream0(HttpURLConnection.java:1607)
        at sun.net.www.protocol.http.HttpURLConnection.getInputStream(HttpURLConnection.java:1441)
        at java.net.HttpURLConnection.getResponseCode(HttpURLConnection.java:480)
```

Using `http.auth.preference` you can force Java to use basic authentication instead of NTLM.  Making your call to `sbt-launch.jar` like this.

```
SBT_OPTS="-Xms512M -Xmx1536M -Xss1M -XX:+CMSClassUnloadingEnabled -XX:MaxPermSize=256M"
SBT_OPTS="$SBT_OPTS -Dhttp.proxyHost=myproxy -Dhttp.proxyPort=8080 -Dhttp.proxyUser=username -Dhttp.proxyPassword=mypassword"
SBT_OPTS="$SBT_OPTS -Dhttp.auth.preference=basic"
java $SBT_OPTS -jar `dirname $0`/sbt-launch.jar "$@"
```
