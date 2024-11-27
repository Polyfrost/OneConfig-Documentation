---
description: How to add OneConfig to your mod
---

# Getting Started

{% hint style="danger" %}
This is **NOT** a guide on how to start with modding or set up a modding template. There is documentation for every version of Minecraft that we support on how to set up a mod on their loader.

For Forge 1.8.9 and 1.12.2: [https://moddev.nea.moe/ide-setup/](https://moddev.nea.moe/ide-setup/)

For Forge (modern): [https://docs.minecraftforge.net/en/latest/gettingstarted/](https://docs.minecraftforge.net/en/latest/gettingstarted/)

For Fabric: [https://fabricmc.net/wiki/tutorial:start#creating\_your\_first\_mod](https://fabricmc.net/wiki/tutorial:start#creating_your_first_mod)

For NeoForge: [https://docs.neoforged.net/docs/gettingstarted/](https://docs.neoforged.net/docs/gettingstarted/)

From there, instead of using the default templates of those loaders, you would use the [OneConfigExampleMod](https://github.com/Polyfrost/OneConfigExampleMod).
{% endhint %}

## OneConfig Example Mod

If you're just starting out or need more advanced features like multiple versions, we highly recommend looking at our [example mod](https://github.com/Polyfrost/OneConfigExampleMod/).

## Including OneConfig yourself

If you don't want to use our mod template, or wish to include OneConfig in one of your new or existing mods, add this to your `build.gradle(.kts)`.

{% hint style="info" %}
While you’re here, we recommend using [Deftu's Gradle Toolkit](https://github.com/Deftu/Gradle-Toolkit), which automatically configures everything in your project for you, including OneConfig.

The toolkit works for all Minecraft versions from 1.8.9 - latest, and supports Forge, Fabric and NeoForge. Setting it up is as simple as applying the appropriate plugins for your needs and configuring the required configuration options. DGT supports complicated setups such as multi-version projects with absolute ease.

It also provides several smaller utilities for things such as authenticating your Minecraft/Microsoft account in the developer environment via [DevAuth](https://github.com/DJtheRedstoner/DevAuth) or setting up your own Forge coremod.
{% endhint %}



### Available modules

OneConfig's functionality is split into several modules for ease of use and to improve the developer experience. When making a mod using OneConfig, you will need to individually select modules you will be utilizing within your mod in order to gain access to their functionality, and the platform / Minecraft version-specific implementation of OneConfig.

<table><thead><tr><th width="237">Module</th><th width="436">Purpose</th></tr></thead><tbody><tr><td><code>commands</code></td><td>The tree based command system used in OneConfig.</td></tr><tr><td><code>config</code></td><td>The tree based configuration system used in OneConfig.</td></tr><tr><td><code>config-impl</code></td><td>The default implementation of the configuration system used in OneConfig.</td></tr><tr><td><code>events</code></td><td>The event system used in OneConfig.</td></tr><tr><td><code>hud</code></td><td>The HUD system used in OneConfig.</td></tr><tr><td><code>internal</code></td><td>OneConfig's UI implementation.</td></tr><tr><td><code>ui</code></td><td>The UI system used in OneConfig.</td></tr><tr><td><code>utils</code></td><td>Various utilities used in OneConfig.</td></tr></tbody></table>

### Setting up your build files

{% tabs %}
{% tab title="Groovy (DGT)" %}
<pre class="language-gradle"><code class="lang-gradle"><strong>toolkitLoomHelper {
</strong><strong>    useOneConfig(mcData, "commands", "events", "ui")
</strong><strong>
</strong>    if (mcData.isLegacyForge) {
        useTweaker("org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker", GameSide.CLIENT)    
    }
}

repositories {
    maven { url 'https://repo.polyfrost.org/releases' }
}
</code></pre>
{% endtab %}

{% tab title="Kotlin (DGT)" %}
```kts
toolkitLoomHelper {
    useOneConfig(mcData, "commands", "events", "ui")

    if (mcData.isLegacyForge) {
        useTweaker("org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker", GameSide.CLIENT)    
    }
}

repositories {
    maven("https://repo.polyfrost.org/releases")
}
```
{% endtab %}

{% tab title="Groovy (Normal)" %}
```gradle
loom {
    launchConfigs {
        client {
            // Loads OneConfig in dev env. Replace other tweak classes with this, but keep any other attributes!
            arg("--tweakClass", "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker")
        }
    }
}

repositories {
    maven { url 'https://repo.polyfrost.org/releases' }
}

dependencies {
    // `include` should be replaced with a configuration that includes your dependencies in the JAR

    // Basic OneConfig dependencies for legacy versions. See OneConfig example mod for more info
    def oneConfigMcVersion = "1.8.9"
    def oneConfigModLoader = "forge"
    def oneConfigModules = ["commands", "events", "ui"] // Refer to possible modules above
    def oneconfigVersion = "+"
    for (String module : oneConfigModules + "${oneConfigMcVersion}-${oneConfigModLoader}") {
        compileOnly('org.polyfrost.oneconfig:${module}:${oneConfigVersion}') // Should NOT be included in JAR
    }
    
    def loaderModule = "launchwrapper" // "fabriclike" for Fabric and Quilt, "launchwrapper" for versions 1.8.9 - 1.12.2, "modlauncher" for Forge 1.13+
    def loaderVersion = "+" // "+" resolves the latest version. You can specify a set version here.
    include('org.polyfrost.oneconfig:stage0:$loaderModule:$loaderVersion') // Should be included in JAR
}

jar { // loads OneConfig at launch. Add these launch attributes but keep your old attributes!
    manifest.attributes(
            "ModSide": "CLIENT",
            "TweakOrder": "0",
            "ForceLoadAsMod": true,
            "TweakClass": "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker",
    )
}
```


{% endtab %}

{% tab title="Kotlin (Normal)" %}
```kts
loom {
    launchConfigs.named("client") {
        arg("--tweakClass", "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker")
    }
}

repositories {
    maven("https://repo.polyfrost.org/releases")
}

dependencies {
    // `include` should be replaced with a configuration that includes your dependencies in the JAR

    // Basic OneConfig dependencies for legacy versions. See OneConfig example mod for more info
    val oneConfigMcVersion = "1.8.9"
    val oneConfigModLoader = "forge"
    val oneConfigModules = arrayOf("commands", "events", "ui") // Refer to possible modules above
    val oneconfigVersion = "+"
    for (module in (oneConfigModules + "$oneConfigMcVersion-$oneConfigModLoader")) {
        compileOnly("org.polyfrost.oneconfig:$module:$oneConfigVersion") // Should NOT be included in JAR
    }
    
    def loaderModule = "launchwrapper" // "fabriclike" for Fabric and Quilt, "launchwrapper" for versions 1.8.9 - 1.12.2, "modlauncher" for Forge 1.13+
    def loaderVersion = "+" // "+" resolves the latest version. You can specify a set version here.
    include("org.polyfrost.oneconfig:stage0:$loaderModule:$loaderVersion") // Should be included in JAR
}

tasks {
    jar { // loads OneConfig at launch. Add these launch attributes but keep your old attributes!
        manifest.attributes += mapOf(
            "ModSide" to "CLIENT",
            "TweakOrder" to 0,
            "ForceLoadAsMod" to true,
            "TweakClass" to "org.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker"
        )
    }
}
```


{% endtab %}
{% endtabs %}

