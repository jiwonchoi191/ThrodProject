> **Warning**
> This sample has been migraated to the new [platform-samples repository](https://github.com/android/platform-samples)
> and will no longer be maintained. 
> 
> Please use the following
>[sample](https://github.com/android/platform-samples/tree/main/samples/user-interface/text/src/main/java/com/example/platform/ui/text/DownloadableFonts.kt)
> instead.
>
> Thank you for your understanding.

Android DownloadableFonts Sample (Kotlin)
===================================

This sample demonstrates how to use the Downloadable Fonts feature introduced in Android O.
Downloadable Fonts is a feature that allows apps to request a certain font from a provider
instead of bundling it or downloading it themselves. This means, there is no need to bundle the
font as an asset.

Introduction
------------

There are two ways of requesting a font to download.
To request a font to download from Java code, you need to create a [FontRequest][1] class first like
this:
```java

```
The parameters `ProviderAuthority`, `ProviderPackage` are given by a font provider, in the case
above uses Google Play Services as a font provider.
The third parameter is a query string about the requested font. The syntax of the query is defined
by the font provider.

Then pass the request instance to the `requestFont` method in the [FontsContractCompat][2].
```java

```
The downloaded font or an error code if the request failed will be passed to the callback.
The example above assumes you are using the classes from the support library. There are
corresponding classes in the framework, but the feature is available back to API level 14 if you
use the support library.

You can declare a downloaded font in an XML file and let the system download it for you and use it
in layouts.
```xml
<font-family xmlns:app="http://schemas.android.com/apk/res-auto"
        app:fontProviderAuthority="com.google.android.gms.fonts"
        app:fontProviderPackage="com.google.android.gms"
        app:fontProviderQuery="Lobster Two"
        app:fontProviderCerts="@array/com_google_android_gms_fonts_certs">
</font-family>
```
By defining the requested font in an XML file and putting the `preloaded_fonts` array and the
meta-data tag in the AndroidManifest, you can avoid the delay until the font is downloaded by the
first attempt.
```xml
<resources>
    <array name="preloaded_fonts" translatable="false">
        <item>@font/lobster_two</item>
    </array>
</resources>
```

```xml
<application >
    ...
    <meta-data android:name="preloaded_fonts" android:resource="@array/preloaded_fonts" />
    ...
</application>
```

Note that the sample uses Google Play Services as a font provider, which requires pre-released
version of Google Play Services.
You can sign up for the beta program so that the beta version of Google Play Services is
downloaded to your device. https://developers.google.com/android/guides/beta-program
If you have Google Play Services whose version number is equal or above 11.x.x, that means you
have the compatible version installed. (You can confirm by navigating to
Settings -> Apps -> Google Play Services)

[1]: https://developer.android.com/reference/android/support/v4/provider/FontRequest.html
[2]: https://developer.android.com/reference/android/support/v4/provider/FontsContractCompat.html

Pre-requisites
--------------

- Android SDK 25
- Android Build Tools v25.0.3
- Android Support Repository

Screenshots
-------------

<img src="screenshots/screenshot-1.png" height="400" alt="Screenshot"/> 

Getting Started
---------------

This sample uses the Gradle build system. To build this project, use the
"gradlew build" command or use "Import Project" in Android Studio.

Support
-------

- Stack Overflow: http://stackoverflow.com/questions/tagged/android

If you've found an error in this sample, please file an issue:
https://github.com/android/user-interface

Patches are encouraged, and may be submitted by forking this project and
submitting a pull request through GitHub. Please see CONTRIBUTING.md for more details.
