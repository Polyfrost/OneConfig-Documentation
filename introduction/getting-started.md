---
description: How to add OneConfig to your mod
---

# Getting started

{% hint style="danger" %}
This is **NOT** a guide on how to start with modding or set up a modding template. There is documentation for every version of Minecraft that we support on how to set up a mod on their loader.

For Forge 1.8.9 and 1.12.2: [https://moddev.nea.moe/ide-setup/](https://moddev.nea.moe/ide-setup/)

For Forge (modern): [https://docs.minecraftforge.net/en/latest/gettingstarted/](https://docs.minecraftforge.net/en/latest/gettingstarted/)

For Fabric: [https://fabricmc.net/wiki/tutorial:start#creating\_your\_first\_mod](https://fabricmc.net/wiki/tutorial:start#creating_your_first_mod)

For NeoForge: [https://docs.neoforged.net/docs/gettingstarted/](https://docs.neoforged.net/docs/gettingstarted/)

From there, instead of using the default templates of those loaders, you would use the [OneConfigExampleMod](https://github.com/Polyfrost/OneConfigExampleMod).
{% endhint %}

## OneConfig Example Mod

If you're just starting out or need more advanced features like multiple versions, we highly recommend looking at our [example mod](https://github.com/Polyfrost/OneConfigExampleMod/). When cloning the example mod, please choose from one of the following branches:

<table><thead><tr><th width="158">Branch</th><th width="173">Versions</th><th width="142" data-type="checkbox">Preprocessor?</th><th width="85" data-type="checkbox">DGT?</th><th>Notes</th></tr></thead><tbody><tr><td>multi-version</td><td>All OneConfig-supported versions (1.8.9-Latest, Fabric/Forge)</td><td>true</td><td>true</td><td>You can always clone this branch and remove all but a single version, in case you want to tackle multiversion later.</td></tr><tr><td>legacy-forge</td><td>1.8.9 Forge</td><td>false</td><td>true</td><td></td></tr><tr><td>legacy-fabric</td><td>1.8.9 Fabric</td><td>false</td><td>true</td><td></td></tr><tr><td>modern-fabric</td><td>Latest Fabric</td><td>false</td><td>true</td><td></td></tr><tr><td>modern-forge</td><td>Latest Forge</td><td>false</td><td>true</td><td></td></tr><tr><td>kotlin-[branch]</td><td>N/A</td><td>true</td><td>true</td><td>Each branch has a Kotlin version.</td></tr></tbody></table>

## Including OneConfig yourself

If you don't want to use our mod template, or wish to include OneConfig in one of your new or existing mods, add this to your `build.gradle(.kts)`.

{% hint style="info" %}
While you’re here, we recommend using [Deftu's Gradle Toolkit](https://github.com/Deftu/Gradle-Toolkit), which automatically configures everything in your project for you, including OneConfig. DGT is included in our example mod template.

The toolkit works for all Minecraft versions from 1.8.9 - latest, and supports Forge, Fabric and NeoForge. Setting it up is as simple as applying the appropriate plugins for your needs and configuring the required configuration options. DGT also supports complicated setups such as multi-version projects.

It also provides several smaller utilities for things such as authenticating your Minecraft/Microsoft account in the developer environment via [DevAuth](https://github.com/DJtheRedstoner/DevAuth) or setting up your own Forge coremod.
{% endhint %}



### Available modules

OneConfig's functionality is split into several modules for ease of use and to improve the developer experience. When making a mod using OneConfig, you will need to individually select modules you will be utilizing within your mod in order to gain access to their functionality, and the platform / Minecraft version-specific implementation of OneConfig.

<table><thead><tr><th width="237">Module</th><th width="436">Purpose</th></tr></thead><tbody><tr><td><code>commands</code></td><td>The tree based command system used in OneConfig.</td></tr><tr><td><code>config</code></td><td>The tree based configuration system used in OneConfig.</td></tr><tr><td><code>config-impl</code></td><td>The default implementation of the configuration system used in OneConfig.</td></tr><tr><td><code>events</code></td><td>The event system used in OneConfig.</td></tr><tr><td><code>hud</code></td><td>The HUD system used in OneConfig.</td></tr><tr><td><code>internal</code></td><td>OneConfig's UI implementation.</td></tr><tr><td><code>ui</code></td><td>The UI system used in OneConfig.</td></tr><tr><td><code>utils</code></td><td>Various utilities used in OneConfig.</td></tr></tbody></table>

### Setting up your build files

{% tabs %}
{% tab title="Kotlin (DGT)" %}
```kts
toolkitLoomHelper {
    useOneConfig {
        version = "1.0.0-alpha.49" // Put whatever the latest is here
        loaderVersion = "1.1.0-alpha.35" // Put whatever the latest is here

        usePolyMixin = true // If you want to use Mixin on Legacy Forge, you need PolyMixin
        polyMixinVersion = "0.8.4+build.2" // If you want to use Mixin on Legacy Forge, you need PolyMixin

        applyLoaderTweaker = true // Set this to false if you want to use a custom tweaker.

        for (module in arrayOf("commands", "events", "ui")) {
            +module
        }
    }
}
```
{% endtab %}

{% tab title="Kotlin (Normal)" %}
```kts
loom {
    launchConfigs.named("client") {
        if (platform.isLegacyForge) { // If Forge and MC is 1.12.2 or below
            // Loads OneConfig in dev env. Replace other tweak classes with this, but keep any other attributes!
            arg("--tweakClass", "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker")
        }
    }
}

repositories {
    maven("https://repo.polyfrost.org/releases")
    maven("https://repo.polyfrost.org/snapshots") // Remove when OneConfig is out of beta
}

dependencies {
    // `include` should be replaced with a configuration that includes your dependencies in the JAR
    
    // Basic OneConfig dependencies for legacy versions. See OneConfig example mod for more info
    val oneConfigMcVersion = "1.8.9"
    val oneConfigModLoader = "forge"
    val oneConfigModules = arrayOf("commands", "events", "ui") // Refer to possible modules above
    val oneconfigVersion = "1.0.0-alpha.49" // Put whatever the latest is here
    for (module in oneConfigModules) {
        if (platform.isLegacyForge) {
            compileOnly("org.polyfrost.oneconfig:$module:$oneConfigVersion") // Should NOT be included in JAR
        } else {
            implementation("org.polyfrost.oneconfig:$module:$oneConfigVersion") // Should NOT be included in JAR
        }
    }
    
    if (platform.isLegacyForge) {
        val loaderModule = "launchwrapper"
        val loaderVersion = "1.1.0-alpha.35" // Put whatever the latest is here
        include("org.polyfrost.oneconfig:stage0:$loaderModule:$loaderVersion") // Should be included in JAR
        
        modCompileOnly("org.polyfrost.oneconfig:$oneConfigMcVersion-$oneConfigModLoader:$oneConfigVersion")
    } else {
        modImplementation("org.polyfrost.oneconfig:$oneConfigMcVersion-$oneConfigModLoader:$oneConfigVersion")
    }
}

tasks {
    jar { // loads OneConfig at launch. Add these launch attributes but keep your old attributes!
        if (platform.isLegacyForge) {
            manifest.attributes += mapOf(
                "ModSide" to "CLIENT",
                "TweakOrder" to 0,
                "ForceLoadAsMod" to true,
                "TweakClass" to "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker"
            )
        }
    }
}
```


{% endtab %}

{% tab title="Groovy (DGT)" %}
<pre class="language-gradle"><code class="lang-gradle"><strong>toolkitLoomHelper {
</strong>    useOneConfig {
        version = "1.0.0-alpha.49" // Put whatever the latest is here
        loaderVersion = "1.1.0-alpha.35" // Put whatever the latest is here

        usePolyMixin = true // If you want to use Mixin on Legacy Forge, you need PolyMixin
        polyMixinVersion = "0.8.4+build.2" // If you want to use Mixin on Legacy Forge, you need PolyMixin

        applyLoaderTweaker = true // Set this to false if you want to use a custom tweaker.

        for (String module : ["commands", "events", "ui"]) {
            addModule(module)
        }
    }
}
</code></pre>
{% endtab %}

{% tab title="Groovy (Normal)" %}
```gradle
loom {
    launchConfigs {
        client {
            if (platform.isLegacyForge) { // If Forge and MC is 1.12.2 or below
                // Loads OneConfig in dev env. Replace other tweak classes with this, but keep any other attributes!
                arg("--tweakClass", "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker")
            }
        }
    }
}

repositories {
    maven { url 'https://repo.polyfrost.org/releases' }
    maven { url 'https://repo.polyfrost.org/snapshots' } // Remove when OneConfig is out of beta
}

dependencies {
    // `include` should be replaced with a configuration that includes your dependencies in the JAR

    // Basic OneConfig dependencies for legacy versions. See OneConfig example mod for more info
    def oneConfigMcVersion = "1.8.9"
    def oneConfigModLoader = "forge"
    def oneConfigModules = ["commands", "events", "ui"] // Refer to possible modules above
    def oneconfigVersion = "1.0.0-alpha.49" // Put whatever the latest is here
    for (String module : oneConfigModules) {
        if (platform.isLegacyForge) {
            compileOnly('org.polyfrost.oneconfig:${module}:${oneConfigVersion}') // Should NOT be included in JAR
        } else {
            implementation('org.polyfrost.oneconfig:${module}:${oneConfigVersion}') // Should NOT be included in JAR
        }
    }
    
    if (platform.isLegacyForge) {
        def loaderModule = "launchwrapper"
        def loaderVersion = "1.1.0-alpha.35" // Put whatever the latest is here
        include('org.polyfrost.oneconfig:stage0:$loaderModule:$loaderVersion') // Should be included in JAR
        
        modCompileOnly('org.polyfrost.oneconfig:${oneConfigMcVersion}-${oneConfigModLoader}:${oneConfigVersion}')
    } else {
        modImplementation('org.polyfrost.oneconfig:${oneConfigMcVersion}-${oneConfigModLoader}:${oneConfigVersion}')
    }
}

jar { // loads OneConfig at launch. Add these launch attributes but keep your old attributes!
    if (platform.isLegacyForge) {
        manifest.attributes(
                "ModSide": "CLIENT",
                "TweakOrder": "0",
                "ForceLoadAsMod": true,
                "TweakClass": "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker",
        )
    }
}
```


{% endtab %}
{% endtabs %}

