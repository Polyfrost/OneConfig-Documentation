---
description: How to include OneConfig in your project
---

# Including OneConfig

If you haven't used our Mod template, are switching to OneConfig, or you just want to include OneConfig into your mod, add this to your build.gradle(.kts):

{% hint style="warning" %}
OneConfig utilizes features that require a Java 17+ Gradle VM alongside the Java 8 VM for your mod. If you are unsure about how to set these individually, check out [project-setup.md](basics/project-setup.md "mention") for more information on it (you can just select your VM if you already have one instead of downloading)
{% endhint %}

{% tabs %}
{% tab title="Groovy" %}
```groovy
repositories {
    maven { url 'repo.polyfrost.cc/releases' }
}

dependencies {
    compileOnly('cc.polyfrost:oneconfig-1.8.9-forge:1') // Should not be included in jar
    include('cc.polyfrost:oneconfigwrapper-1.8.9-forge:1') // Should be included in jar
}

jar { // load OneConfig at launch
    manifest.attributes(
            "ModSide": "CLIENT",
            "TweakOrder": 0,
            "ForceLoadAsMod": true,
            "FMLCorePlugin": "cc.polyfrost.oneconfigwrapper.OneConfigWrapper",
            "FMLCorePluginContainsFMLMod": "yes"
    )
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kts
repositories {
    maven("repo.polyfrost.cc/releases")
}

dependencies {
    compileOnly("cc.polyfrost:oneconfig-1.8.9-forge:1") // Should not be included in jar
    include("cc.polyfrost:oneconfigwrapper-1.8.9-forge:1") // Should be included in jar
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

Easy as that! Now rebuild your project, and enjoy all the things OneConfig has to offer!
