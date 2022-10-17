---
description: (aka "How the hell do I add OneConfig to my mod?")
---

# Getting Started

If you're unfamiliar with Java, or Minecraft Modding, please read [Modding Basics](including-oneconfig.md) first. It's a fantastic beginner's guide.

Also, if you have any issues with the example mod or implementing OneConfig, [join our Discord](https://inv.wtf/polyfrost) and open a developer ticket in the [#support](https://discord.com/channels/822066990423605249/984977983439794176) channel.

### OneConfig's Example Mod

If you're just starting out, we highly recommend looking at our [example mod](https://github.com/Polyfrost/OneConfigExampleMod/). Please follow the instructions on how to do that in the template's [README](https://github.com/Polyfrost/OneConfigExampleMod/blob/main/README.md). This documentation is here for a reason

### Including OneConfig Yourself

If you want to avoid using our own [mod template](https://github.com/Polyfrost/OneConfigExampleMod/), or wish to include OneConfig in one of your new or existing mods, add this to your `build.gradle(.kts)`

{% tabs %}
{% tab title="Groovy" %}
```groovy
repositories {
    maven { url 'repo.polyfrost.cc/releases' }
}

dependencies {
    compileOnly('cc.polyfrost:oneconfig-1.8.9-forge:0.1.0-alpha+') // Should not be included in jar
    include('cc.polyfrost:oneconfig-wrapper-launchwrapper:1.0.0-alpha+') // Should be included in jar
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
    compileOnly("cc.polyfrost:oneconfig-1.8.9-forge:0.1.0-alpha+") // Should not be included in jar
    include("cc.polyfrost:oneconfig-wrapper-launchwrapper:1.0.0-alpha+") // Should be included in jar
}

tasks {
    jar {
        manifest.attributes {
            "ModSide" to "CLIENT",
            "TweakOrder" to 0,
            "ForceLoadAsMod" to true,
            "TweakClass" to "cc.polyfrost.oneconfigwrapper.OneConfigWrapper"
        }
    }
}
```
{% endtab %}
{% endtabs %}
