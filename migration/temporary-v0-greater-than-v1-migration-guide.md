# Temporary V0->V1 Migration Guide

OneConfig V1 is now available to all developers, with some conditions:

* Not everything has been documented just yet...
* Currently, V1 will not work on modern versions due to an issue with LWJGL natives. But it compiles!
* Expect bugs with OneConfig V1 itself.

This is in **NO WAY** a complete guide as of yet. [**PLEASE** contribute to this guide](https://github.com/Polyfrost/OneConfig-Documentation/tree/v1) if you find any discrepancies.&#x20;

Below are screenshots of the new GUI. Yes, these are concept designs, but it's basically been implemented 1:1 and I'm way too lazy to take actual screenshots lol

<figure><img src="../.gitbook/assets/image.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

## Get it working in Gradle

Please follow the [Getting Started](../introduction/getting-started.md) guide for this.

## Notable changes

This is in **NO WAY** a complete guide as of yet. [**PLEASE** contribute to this guide](https://github.com/Polyfrost/OneConfig-Documentation/tree/v1) if you find any discrepancies.&#x20;

### New

<pre><code>Now split into multiple, non-Minecraft dependant modules, and one Minecraft module
<strong>Uses PolyUI
</strong><strong>  - Extremely optimized UI lib, using NanoVG
</strong><strong>  - "Render what you need ONLY WHEN you need it"
</strong><strong>    - Performance boost as a result of this
</strong>  - As a result, theming support is automatic and will be implemented soon
Official support for Legacy Fabric and modern MC (Forge, Fabric, and soon NeoForge)
Commands can now be created via `CommandBuilder`, a Brigadier-style builder.
Complete rewrite of config system
  -https://github.com/Polyfrost/OneConfig/tree/v1/modules/config#oneconfig-config
  - Now supports more than just registering config values via annotations
Complete rewrite of HUD system
  - Using PolyUI
  - Separate from configs now
  - Supports multiple of a HUD
  - https://github.com/Polyfrost/OneConfig/tree/v1/modules/hud#oneconfig-hud
  - As explained, you can use `LegacyHud` to just render like in V0. But we STRONGLY recommend using the new PolyUI-based APIs
<strong>Keybind rewrite
</strong></code></pre>

### Package changes

You should be able to do a find and replace with `import <old package name>` . Go in opposite order from this list if you want to do a full search and replace.

```
cc.polyfrost -> org.polyfrost
cc.polyfrost.libs.universal -> org.polyfrost.universal
cc.polyfrost.oneconfig.events -> org.polyfrost.oneconfig.api.event.v1.events
cc.polyfrost.oneconfig.platform -> org.polyfrost.oneconfig.api.platform.v1
cc.polyfrost.oneconfig.utils -> org.polyfrost.oneconfig.utils.v1
cc.polyfrost.oneconfig.utils (for Notifications class) -> org.polyfrost.oneconfig.api.ui.v1
cc.polyfrost.oneconfig.utils.hypixel -> org.polyfrost.oneconfig.api.hypixel.v0
cc.polyfrost.oneconfig.utils.commands -> org.polyfrost.oneconfig.api.commands.v1
cc.polyfrost.oneconfig.utils.commands.annotations -> org.polyfrost.oneconfig.api.commands.v1.factories.annotated
cc.polyfrost.oneconfig.config -> org.polyfrost.oneconfig.api.config.v1
```

### Class name changes

```
@Main and @SubCommand -> @Command
@Description -> @Parameter
@Greedy -> `greedy` field in @Command annotation
OneColor -> PolyColor
new OneColor(value) -> ColorUtils.rgba(value)
NetworkUtils.getJsonElement -> JsonUtils.parseFromUrl
JsonUtils.parseString -> `parse` or `parseOrNull`
EventManager.register notes:
- We strongly recommend devs to switch from annotation-based event registering to the new system.
  - EventManager.register(EventName.class, (event) -> { doStuff(); });
  - In Kotlin you can do eventHandler { event: EventName -> { doStuff() } }.register()
- If for whatever reason you cannot, keep the following in mind:
  - Registered objects to the EventManager are now not removable by default. To allow it to be removed, call `register(new ClassName(), true)`
TickDelay -> EventDelay.ticks
RenderTickDelay -> EventDelay.render

```

### Misc

<pre><code><strong>CommandManager.INSTANCE.registerCommand -> CommandManager.registerCommand
</strong>CommandManager.INSTANCE.addParser -> CommandManager.INSTANCE.registerParser
@Command `aliases` field -> `value`
- it is now an array, you pass the main one as the first and the rest as aliases
<strong>Notifications.INSTANCE.send -> NotificationsManager.INSTANCE.enqueue
</strong><strong>- You now need to provide a notification "type"
</strong><strong>- We'll probably rename the class back to Notifications depending on how things go
</strong>Multithreading.runAsync -> Multithreading.submit
ConfigUtils.getProfileFile -> ConfigManager.active().getFolder().resolve
- Returns a Path instead of a File
HypixelUtils.INSTANCE -> HypixelUtils
- Locraw Util is completely removed, instead we now provide a Hypixel Mod API-based API in HypixelUtils
ArgumentParser.complete -> getAutoCompletions
- It is now nullable, so pass `null` instead of an empty list
- For config annotations, the `name` field is now `title`
- For config annotations, `size` is removed. All config options are "size 2"
- **VERY IMPORTANT** - variables in configs are NOT serialized by default anymore. Instead of @Exclude-ing variables you don't want, you need to @Include variable you DO want and not annotate the others.
- new VigilanceMigrator (or any other migrator) -> `loadFrom` method in config.
- @VigilanceName (or any other migrator name -> @PreviousName (check javadocs for new syntax)
- `initialize` method is no longer necessary.
- addListener -> addCallback
</code></pre>

## Examples

We recommend checking out our mods, which have somewhat already been ported to V1 (59%). Good examples are [CrashPatch](https://github.com/Polyfrost/CrashPatch/tree/twoconfig), [EvergreenHUD](https://github.com/Polyfrost/EvergreenHUD/tree/rewrite), and [Hytils Reborn](https://github.com/Polyfrost/Hytils-Reborn/tree/twoconfig). Here is a periodically updated list of our ported mods:

```
- CrashPatch [V1 DONE]
- PolyBlur [V1 DONE]
- ColorSaturation [V1 DONE]
- OverflowAnimations [V1 DONE]
- GlintColorizer [V1 DONE]
- PolyPatcher [V1 DONE]
- REDACTION [V1 DONE]
- PolySprint [V1 DONE]
- BehindYouV3 [V1 ½ done]
- PolyCrosshair [V1 __not__ done]
- OverflowParticles [V1 __not__ done]

- EvergreenHUD [V1 ½ done]
- PolyHitbox [V1 __not__ done]
- VanillaHUD [V1 ½ DONE]
- Chatting [V1 __not__ done]
- Keystrokes Reborn [V1 __not__ done]

- PolyNametag [V1 DONE]

- DamageTint [V1 DONE]
- Hytils Reborn [V1 DONE]

- PolyTime [V1 DONE]
- PolyWeather [V1 DONE]
```

All the ported versions should be in the "twoconfig" branch (EXCEPT EvergreenHUD, that work is in the "rewrite" branch).
