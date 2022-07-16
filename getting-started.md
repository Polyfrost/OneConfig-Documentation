---
description: (aka "How the hell do I add OneConfig to my mod?")
---

# Getting Started

If you are **not** familiar with Minecraft modding and Java, **please skip to** [**Modding Basics**](including-oneconfig.md)**.**

**If you have ANY issues with our example mod or including OneConfig,** [**join our Discord**](https://inv.wtf/polyfrost) **and open a developer ticket in the** [**#support**](https://discord.com/channels/822066990423605249/984977983439794176) **channel.**

## Including OneConfig

If you:

* do not wish to use our [**mod template**](getting-started.md#oneconfigs-example-mod),
* are switching to OneConfig, or&#x20;
* you just want to include OneConfig into your mod;

add this to your `build.gradle(.kts)`:

{% tabs %}
{% tab title="Groovy" %}
```groovy
repositories {
    maven { url 'repo.polyfrost.cc/releases' }
}

dependencies {
    compileOnly('cc.polyfrost:oneconfig-1.8.9-forge:1.0.0-alpha+') // Should not be included in jar
    include('cc.polyfrost:oneconfig-wrapper-launchwrapper:0.1.0-alpha+') // Should be included in jar
}

jar { // loads OneConfig at launch
    manifest.attributes(
            "ModSide": "CLIENT",
            "TweakOrder": "0",
            "ForceLoadAsMod": true,
            "TweakClass": "cc.polyfrost.oneconfigwrapper.OneConfigWrapper",
    )
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
repositories {
    maven("repo.polyfrost.cc/releases")
}

dependencies {
    compileOnly("cc.polyfrost:oneconfig-1.8.9-forge:1.0.0-alpha+") // Should not be included in jar
    include("cc.polyfrost:oneconfig-wrapper-launchwrapper:0.1.0-alpha+") // Should be included in jar
}

tasks {
    jar {
        manifest.attributes {
            "ModSide" to "CLIENT",
            "TweakOrder" to 0,
            "ForceLoadAsMod" to true,
            "FMLCorePlugin" to "cc.polyfrost.oneconfigwrapper.OneConfigWrapper",
            "FMLCorePluginContainsFMLMod" to "yes"
        }
    }
}
```
{% endtab %}
{% endtabs %}

## OneConfig's Example Mod

If you are starting out fresh, we recommend using our [**OneConfig Example Mod template**](https://github.com/Polyfrost/OneConfigExampleMod/), found on our GitHub. Please follow the instructions on how to do that in the template's [README](https://github.com/Polyfrost/OneConfigExampleMod/blob/main/README.md).
