---
description: (aka "How the hell do I add OneConfig to my mod?")
---

# Getting Started

If you're unfamiliar with Java, or Minecraft Modding, please read [Modding Basics](including-oneconfig.md) first. It's a fantastic beginner's guide.

### OneConfig's Example Mod

If you're just starting out or need more advanced features like multiple versions, we highly recommend looking at our updatdd [example mod](https://github.com/Polyfrost/OneConfigExampleMod/).

## Including OneConfig Yourself

If you want to avoid using our own [mod template](https://github.com/Polyfrost/OneConfigExampleMod/), or wish to include OneConfig in one of your new or existing mods, add this to your `build.gradle(.kts)`

{% tabs %}
{% tab title="Groovy" %}
<pre class="language-groovy"><code class="lang-groovy">loom {
    launchConfigs {
        client {
            // Loads OneConfig in dev env. Replace other tweak classes with this, but keep any other attributes!
            arg("--tweakClass", "cc.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker")
        }
    }
}

repositories {
    maven { url 'https://repo.polyfrost.cc/releases' }
}

dependencies {
<strong>    // Basic OneConfig dependencies for legacy versions. See OneConfig example mod for more info
</strong>    compileOnly('cc.polyfrost:oneconfig-1.8.9-forge:0.2.2-alpha+') // Should not be included in jar
    // include should be replaced with a configuration that includes this in the jar
    include('cc.polyfrost:oneconfig-wrapper-launchwrapper:1.0.0-beta+') // Should be included in jar
}

jar { // loads OneConfig at launch. Add these launch attributes but keep your old attributes!
    manifest.attributes(
            "ModSide": "CLIENT",
            "TweakOrder": "0",
            "ForceLoadAsMod": true,
            "TweakClass": "cc.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker",
    )
}
</code></pre>
{% endtab %}

{% tab title="Kotlin" %}
<pre class="language-kotlin"><code class="lang-kotlin">loom {
    launchConfigs.named("client") {
         // Loads OneConfig in dev env. Replace other tweak classes with this, but keep any other attributes!
         arg("--tweakClass", "cc.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker")
    }
}

repositories {
    maven("https://repo.polyfrost.cc/releases")
}

dependencies {
<strong>    // Basic OneConfig dependencies for legacy versions. See OneConfig example mod for more info
</strong>    compileOnly("cc.polyfrost:oneconfig-1.8.9-forge:0.2.2-alpha+") // Should not be included in jar
    // include should be replaced with a configuration that includes this in the jar
    include("cc.polyfrost:oneconfig-wrapper-launchwrapper:1.0.0-beta+") // Should be included in jar
}

tasks {
    jar { // loads OneConfig at launch. Add these launch attributes but keep your old attributes!
        manifest.attributes += mapOf(
            "ModSide" to "CLIENT",
            "TweakOrder" to 0,
            "ForceLoadAsMod" to true,
            "TweakClass" to "cc.polyfrost.oneconfig.loader.stage0.LaunchWrapperTweaker"
        )
    }
}
</code></pre>
{% endtab %}
{% endtabs %}
