There are two known issues with using Android 2.1 and both have workarounds.

# Classloader issue #

This fix is necessary for all versions of Android before 2.2 Froyo (see [Android issue 5697](http://code.google.com/p/android/issues/detail?id=5697) for more information).

```
// Workaround to get ROME working with Android 2.1 and earlier
Thread.currentThread().setContextClassLoader(getClass().getClassLoader());
```

You've failed to include the workaround if you get the following error:

```
09-06 11:07:41.036: ERROR/AndroidRuntime(228): Uncaught handler: thread main exiting due to uncaught exception
09-06 11:07:41.055: ERROR/AndroidRuntime(228): java.lang.ExceptionInInitializerError
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.io.SyndFeedInput.build(SyndFeedInput.java:123)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.fetcher.impl.HttpURLFeedFetcher.readSyndFeedFromStream(HttpURLFeedFetcher.java:272)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.fetcher.impl.HttpURLFeedFetcher.getSyndFeedFromStream(HttpURLFeedFetcher.java:277)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.fetcher.impl.HttpURLFeedFetcher.retrieveFeed(HttpURLFeedFetcher.java:146)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.androidrome.demo.RssAtomFeedRetriever.retrieveFeed(RssAtomFeedRetriever.java:30)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.androidrome.demo.RssAtomFeedRetriever.getMostRecentNews(RssAtomFeedRetriever.java:18)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.androidrome.demo.FeedListAdapter.<init>(FeedListAdapter.java:27)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.androidrome.demo.MyActivity.createList(MyActivity.java:25)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.androidrome.demo.MyActivity.onCreate(MyActivity.java:18)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1047)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:2459)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2512)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.app.ActivityThread.access$2200(ActivityThread.java:119)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1863)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.os.Handler.dispatchMessage(Handler.java:99)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.os.Looper.loop(Looper.java:123)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at android.app.ActivityThread.main(ActivityThread.java:4363)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at java.lang.reflect.Method.invokeNative(Native Method)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at java.lang.reflect.Method.invoke(Method.java:521)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:860)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:618)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at dalvik.system.NativeStart.main(Native Method)
09-06 11:07:41.055: ERROR/AndroidRuntime(228): Caused by: java.lang.NullPointerException
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at java.util.Properties.load(Properties.java:290)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.io.impl.PropertiesLoader.<init>(PropertiesLoader.java:74)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.io.impl.PropertiesLoader.getPropertiesLoader(PropertiesLoader.java:46)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.io.impl.PluginManager.<init>(PluginManager.java:54)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.io.impl.PluginManager.<init>(PluginManager.java:46)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.feed.synd.impl.Converters.<init>(Converters.java:40)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     at com.google.code.rome.android.repackaged.com.sun.syndication.feed.synd.SyndFeedImpl.<clinit>(SyndFeedImpl.java:59)
09-06 11:07:41.055: ERROR/AndroidRuntime(228):     ... 22 more
```

# JDOM StringIndexOutOfBoundsException #

This fix is necessary for all versions of Android before 2.2 Froyo. The following error shows up on Android 2.1 and earlier:

```
Caused by: java.lang.StringIndexOutOfBoundsException
        at java.lang.String.substring(String.java:1646)
        at org.jdom.input.SAXHandler.startElement(SAXHandler.java:568)
        at org.apache.harmony.xml.ExpatParser.startElement(ExpatParser.java:145)
        at org.apache.harmony.xml.ExpatParser.append(Native Method)
        at org.apache.harmony.xml.ExpatParser.parseFragment(ExpatParser.java:490)
        at org.apache.harmony.xml.ExpatParser.parseDocument(ExpatParser.java:477)
        at org.apache.harmony.xml.ExpatReader.parse(ExpatReader.java:317)
        at org.apache.harmony.xml.ExpatReader.parse(ExpatReader.java:273)
```

This occurs because of a [bug in ExPat](http://www.jdom.org/pipermail/jdom-interest/2009-July/016345.html), Android's default XML-Parser. The fix is to use the patched version of JDOM 1.1.1 which can be found in downloads.

If you are seeing this error, make sure you are using the forked version of JDOM found in the download section. If you continue to see this error, please file a bug report.