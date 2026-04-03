EventBus (Asamm Fork)
=====================
Fork of [greenrobot/EventBus](https://github.com/greenrobot/EventBus) 3.3.1 with critical
bug fixes for modern Android (API 35+, AndroidX, R8 full mode).

The upstream project is no longer actively maintained (last release Feb 2024, 147 open issues).
This fork applies minimal, targeted patches to keep EventBus working with current Android toolchains.

Changes from upstream 3.3.1
---------------------------
**SubscriberMethodFinder** — fix `NoClassDefFoundError` during `register()`:

- Check `@Subscribe` annotation **before** `getParameterTypes()` to avoid unnecessary class loading
  for non-subscriber methods (based on [PR #560](https://github.com/greenrobot/EventBus/pull/560))
- Catch `NoClassDefFoundError` in `getAnnotation()` for methods referencing classes unavailable on
  the current API level (based on [PR #293](https://github.com/greenrobot/EventBus/pull/293))
- Catch `NoClassDefFoundError` in `getParameterTypes()` for methods with parameter types from newer
  API levels (e.g. `PictureInPictureUiState` on API < 35, `ComponentCaller` on API < 35).
  See [issue #737](https://github.com/greenrobot/EventBus/issues/737),
  [issue #726](https://github.com/greenrobot/EventBus/issues/726)
- Add null-check in `moveToSuperclass()` after `getSuperclass()`
  (based on [PR #560](https://github.com/greenrobot/EventBus/pull/560))

Add to your project
-------------------
[![](https://jitpack.io/v/asamm/EventBus.svg)](https://jitpack.io/#asamm/EventBus)

Available via [JitPack](https://jitpack.io/#asamm/EventBus).

Add the JitPack repository (if not already present):
```kotlin
// settings.gradle.kts
repositories {
    maven(url = "https://jitpack.io")
}
```

Android projects:
```kotlin
implementation("com.github.asamm.EventBus:eventbus-android:3.5.0")
```

Java-only projects:
```kotlin
implementation("com.github.asamm.EventBus:eventbus-java:3.5.0")
```

R8, ProGuard
------------
This library ships [with embedded rules](/eventbus-android/consumer-rules.pro).

Upstream documentation
----------------------
For general EventBus usage, see the [original documentation](https://greenrobot.org/eventbus/documentation/).

License
-------
Copyright (C) 2012-2021 Markus Junginger, greenrobot (https://greenrobot.org)

EventBus binaries and source code can be used according to the [Apache License, Version 2.0](LICENSE).
