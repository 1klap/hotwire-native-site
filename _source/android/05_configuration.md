---
permalink: /android/configuration.html
order: 05
title: "Configuration"
description: "How to customize a Hotwire Native Android app."
---

# Configuration

## Create an Application Instance

Customize your app by configuring options before your `HotwireActivity` instance is created by the system. We recommend using an `Application` instance to place the configuration code.


```kotlin
class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()

        // Set configuration options
    }
}
```

To ensure this invoked when the app starts, add the name of your `Application` instance to `AndroidManifest.xml` via the `android:name` property on the `<application>` node.
p

```xml
<application android:name=".MyApplication">
    <!-- ... -->
</application>
```

## Options

Enable debugging in debug builds:

```kotlin
Hotwire.config.debugLoggingEnabled = BuildConfig.DEBUG
Hotwire.config.webViewDebuggingEnabled = BuildConfig.DEBUG
```

Set the default fragment destination:

```kotlin
Hotwire.defaultFragmentDestination = HotwireWebFragment::class
```

Register fragment destinations:

```kotlin
Hotwire.registerFragmentDestinations(
    MyCustomFragment::class
)
```

Register bridge components, where the first argument is the component name to match in Stimulus:

```kotlin
Hotwire.registerBridgeComponents(
    BridgeComponentFactory("my-custom", ::MyCustomComponent)
)
```

Set the JSON converter used for bridge components:

```kotlin
Hotwire.config.jsonConverter = KotlinXJsonConverter()
```

Customize the user agent:

```kotlin
Hotwire.config.applicationUserAgentPrefix = "My Application;"
```

Set a custom user agent application prefix for every `WebView` instance. The library will automatically append a substring to your prefix which includes:
* - "Hotwire Native Android; Turbo Native Android;"
* - "bridge-components: [your bridge components];"
* - The `WebView`'s default Chromium user agent string
