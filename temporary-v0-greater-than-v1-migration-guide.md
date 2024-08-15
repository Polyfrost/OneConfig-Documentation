# Temporary V0->V1 Migration Guide

OneConfig V1 is now available to all developers, with some conditions:

* With these hacks, your mod will only work in the dev environment, as our loader is not done yet.
* Currently, V1 will not work on modern versions due to an issue with LWJGL natives. But it compiles!
* Expect bugs with OneConfig V1 itself.

This guide assumes you use (Essential/Polyfrost) (Arch)Loom 1.6 or higher, with a Kotlin Gradlescript. If you're on an older version, such as 0.10, some method names from Loom will be different.

This is in **NO WAY** a complete guide as of yet. [**PLEASE** contribute to this guide](https://github.com/Polyfrost/OneConfig-Documentation/tree/v1) if you find any discrepancies.&#x20;

## Get it working in Gradle

Add this to build.gradle.kts. These blocks will most definitely exist already in your buildscript, so follow the comments well.

```kts
loom {
    if (project.platform.isLegacyForge) {
        runConfigs { // This is `launchConfigs` in Loom 0.10
            "client" {
                // **REMOVE ANY EXTRA `programArgs` CALLS FROM THIS BLOCK TOO!**
                // On Loom 0.10 this is `arg` instead of `programArgs`
                programArgs("--tweakClass", "org.polyfrost.oneconfig.internal.legacy.OneConfigTweaker")
                programArgs("--tweakClass", "org.spongepowered.asm.launch.MixinTweaker")
            }
        }
    }
}

repositories {
    maven("https://repo.polyfrost.org/snapshots")
    // Put your old repos here, most importantly the Polyfrost releases repo
}

dependencies {
    // REMOVE OLD ONECONFIG + DEPENDENCIES TOO
    val oneconfig = "1.0.0-alpha.21"
    implementation("org.polyfrost.oneconfig:config-impl:$oneconfig")
    implementation("org.polyfrost.oneconfig:commands:$oneconfig")
    implementation("org.polyfrost.oneconfig:events:$oneconfig")
    implementation("org.polyfrost.oneconfig:ui:$oneconfig")
    implementation("org.polyfrost.oneconfig:internal:$oneconfig")
    modImplementation("org.polyfrost.oneconfig:$platform:$oneconfig")
}
```

You should now see the new API and be able to launch in dev env.

## Notable changes

This is in **NO WAY** a complete guide as of yet. [**PLEASE** contribute to this guide](https://github.com/Polyfrost/OneConfig-Documentation/tree/v1) if you find any discrepancies.&#x20;

### New

```
Now split into multiple, non-Minecraft dependant modules, and one Minecraft module
Uses PolyUI
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
Keybind rewrite
  - TODO!!!!!
```

### Package changes

You should be able to do a find and replace with `import <old package name>` . Go in opposite order from this list.

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
<strong>Notifications.INSTANCE.send -> Notifications.INSTANCE.enqueue
</strong><strong>- You now need to provide a notification "type"
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

### Working HUD example

```kotlin
package org.polyfrost.evergreenhud.hud

import net.minecraft.client.Minecraft
import net.minecraft.network.play.server.S19PacketEntityStatus
import org.polyfrost.evergreenhud.ClientDamageEntityEvent
import org.polyfrost.oneconfig.api.config.v1.annotations.Slider
import org.polyfrost.oneconfig.api.config.v1.annotations.Text
import org.polyfrost.oneconfig.api.event.v1.eventHandler
import org.polyfrost.oneconfig.api.event.v1.events.ReceivePacketEvent
import org.polyfrost.oneconfig.api.event.v1.events.TickEvent
import org.polyfrost.oneconfig.api.hud.v1.TextHud


// this prefix and suffix are used in the HUD editor and can be changed by the user (they are implemented as config options)
class Combo : TextHud(prefix = "Combo:", suffix = "blocks") {
    
    // you can include config options here like normal, just as if it was a config. all the methods like addDependency, loadFrom
    // etc all work here as HUD extends from Config.
    @Slider(
        title = "Discard Time",
        min = 0F,
        max = 10F
    )
    var discardTime = 3

    @Text(title = "No Hit Message")
    var noHitMessage = "0"

    // to register this HUD with the system, we can do the following:
    // note that this needs to be done from another class, e.g. the main mod class would have:
    // HudManager.register(Combo())
    // this would ensure that the HUD is registered and can be displayed.

    // note how there is no transient or exclude, as excluding is now the default behavior.
    private var sentAttackTime = 0L
    private var lastHitTime = 0L
    private var lastAttackId = 0
    private var sentAttack = 0
    
    private var currentCombo = 0
        // here, I am using kotlin features to make the code cleaner later in the HUD. 
        // you can just call update() after each set or whatever. update() is what will make the HUD text change.
        set(value) {
            if (field == value) return
            field = value
            update()
        }

    init {
        // using the new kotlin syntax purely because it looks so much nicer.
        eventHandler { (attacker, target): ClientDamageEntityEvent ->
            if (attacker != mc.thePlayer) {
                return@eventHandler
            }
            sentAttack = target.entityId
            sentAttackTime = System.currentTimeMillis()
        }.register()

        eventHandler { event: ReceivePacketEvent ->
            val packet = event.getPacket() as? S19PacketEntityStatus ?: return@eventHandler
            if (packet.opCode.toInt() != 2) return@eventHandler
            val target = packet.getEntity(mc.theWorld) ?: return@eventHandler

            if (sentAttack != -1 && target.entityId == sentAttack) {
                sentAttack = -1
                if (System.currentTimeMillis() - sentAttackTime > 2000L) {
                    sentAttackTime = 0L
                    currentCombo = 0
                    return@eventHandler
                }
                if (lastAttackId == target.entityId) {
                    currentCombo++
                } else {
                    currentCombo = 1
                }
                lastHitTime = System.currentTimeMillis()
                lastAttackId = target.entityId
            } else if (target.entityId == mc.thePlayer.entityId) {
                currentCombo = 0
            }
        }.register()

        eventHandler { _: TickEvent.Start ->
            if (System.currentTimeMillis() - lastHitTime >= discardTime * 1000L) {
                currentCombo = 0
            }
        }.register()
    }

    // these are no longer fields and instead these methods as there is no point in saving them in memory
    // they are just used for the HUD manager.
    override fun category() = Category.COMBAT

    // this method is called WHENEVER update() is called. it is what supplies the text to the HUD.
    override fun getText() = if (currentCombo == 0) noHitMessage else currentCombo.toString()

    // this is the tree ID of the HUD, which is the same as the ID you supply as if it were a config.
    override fun id() = "evergreenhud/combo.json"

    // This is the title of the HUD, it is displayed in the HUD manager.
    override fun title() = "Combo HUD"

    // this HUD does not periodically update, so we return a negative number.
    override fun updateFrequency() = -1L
}
```
