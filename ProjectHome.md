[ROME](https://rome.dev.java.net/) is an open source Java tool for parsing, generating, and publishing RSS and Atom feeds. Android ROME Feed Reader is a repackaging of ROME so that it works on Android devices.

# Android 2.1 and earlier #

Please be aware that Android 2.2 Froyo does not suffer from these issues. So please do testing on Android 2.1 and earlier to ensure that you do not suffer from these issues.

The following fixes work for Android 1.1 and higher.

## Classloader issue ##

This fix is necessary for all versions of Android before 2.2 Froyo (see [Android issue 5697](http://code.google.com/p/android/issues/detail?id=5697) for more information).

```
// Workaround to get ROME working with Android 2.1 and earlier
Thread.currentThread().setContextClassLoader(getClass().getClassLoader());
```

## JDOM StringIndexOutOfBoundsException ##

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