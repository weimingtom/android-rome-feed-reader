# JDOM #

This project requires a forked version of JDOM that is available from [downloads](http://code.google.com/p/android-rome-feed-reader/downloads/detail?name=jdom-1.1.1-android-fork.jar&can=2&q=).

# Maven #

Add the Maven repository hosted on Google Code to your project's pom.xml:

```
<repositories>
  <repository>
    <id>android-rome-feed-reader-repository</id>
    <name>Android ROME Feed Reader Repository</name>
    <url>https://android-rome-feed-reader.googlecode.com/svn/maven2/releases</url>
  </repository>
</repositories>
```

Then add this dependency to your project's pom.xml:

```
<dependency>
  <groupId>com.google.code.android-rome-feed-reader</groupId>
  <artifactId>android-rome-feed-reader</artifactId>
  <version>1.0.0-r2</version>
</dependency>
```

# Ant #

Manually download the feed reader jar from the [download page](http://code.google.com/p/android-rome-feed-reader/downloads/list). You will also need to download JDOM 1.1.1-android-forked from the download page.