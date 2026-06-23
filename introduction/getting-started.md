---
description: How to add OneConfig to your mod
---

# Getting started

{% hint style="danger" %}
This is **NOT** a guide on how to start with modding or set up a modding template. There is documentation for every
version of Minecraft that we support on how to set up a mod on their loader.

For
Fabric: [https://fabricmc.net/wiki/tutorial:start#creating\_your\_first\_mod](https://fabricmc.net/wiki/tutorial:start#creating_your_first_mod)

For NeoForge: [https://docs.neoforged.net/docs/gettingstarted/](https://docs.neoforged.net/docs/gettingstarted/)
{% endhint %}

## Latest versions

<div><figure><img src="https://repo.polyfrost.org/api/badge/latest/snapshots/org/polyfrost/oneconfig/26.1-fabric?color=1452cc&#x26;name=OneConfig" alt=""><figcaption></figcaption></figure>

## OneConfig Example Mod

If you're just starting out or need more advanced features like multiple versions, we highly recommend looking at
our [example mod](https://github.com/Polyfrost/OneConfigExampleMod/). When cloning the example mod, please choose from
one of the following branches:

<table>
 <thead>
  <tr>
   <th width="158">Branch</th>
   <th width="173">Versions</th>
   <th>Notes</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>multi-version</td>
   <td>All OneConfig-supported versions (1.21.1-Latest, Fabric/NeoForge)</td>
   <td>You can always clone this branch and remove all but a single version, in case you want to tackle multiversion later.</td>
  </tr>
  <tr>
   <td>modern-fabric</td>
   <td>Latest Fabric</td>
   <td></td>
  </tr>
  <tr>
   <td>modern-forge</td>
   <td>Latest Forge</td>
   <td></td>
  </tr>
  <tr>
   <td>kotlin-[branch]</td>
   <td>N/A</td>
   <td>Each branch has a Kotlin version.</td>
  </tr>
 </tbody>
</table>

## Including OneConfig yourself

If you don't want to use our mod template, or wish to include OneConfig in one of your new or existing mods, add this to
your `build.gradle(.kts)`.

### Available modules

OneConfig's functionality is split into several modules for ease of use and to improve the developer experience. When
making a mod using OneConfig, you will need to individually select modules you will be utilizing within your mod in
order to gain access to their functionality, and the platform / Minecraft version-specific implementation of OneConfig.

<table>
    <thead>
    <tr>
        <th width="237">Module</th>
        <th width="436">Purpose</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td><code>commands</code></td>
        <td>The tree based command system used in OneConfig.</td>
    </tr>
    <tr>
        <td><code>compose-bundle</code></td>
        <td>Bundles the compose runtime used for rendering.</td>
    </tr>
    <tr>
        <td><code>config</code></td>
        <td>The tree based configuration system used in OneConfig.</td>
    </tr>
    <tr>
        <td><code>config-impl</code></td>
        <td>The default implementation of the configuration system used in OneConfig.</td>
    </tr>
    <tr>
        <td><code>events</code></td>
        <td>The event system used in OneConfig.</td>
    </tr>
    <tr>
        <td><code>hud</code></td>
        <td>The HUD system used in OneConfig.</td>
    </tr>
    <tr>
        <td><code>internal</code></td>
        <td>OneConfig's UI implementation.</td>
    </tr>
    <tr>
        <td><code>poly-compose</code></td>
        <td>Contains important helper functions for the compose rendering.</td>
    </tr>
    <tr>
        <td><code>relocator</code></td>
        <td>A small tool that is used to duplicate code for multiple implementations.</td>
    </tr>
    <tr>
        <td><code>ui</code></td>
        <td>The UI system used in OneConfig.</td>
    </tr>
    <tr>
        <td><code>utils</code></td>
        <td>Various utilities used in OneConfig.</td>
    </tr>
    </tbody>
</table>

### Setting up your build files

{% tabs %}
{% tab title="Kotlin" %}

```kts
repositories {
    maven("https://repo.polyfrost.org/releases")
    maven("https://repo.polyfrost.org/snapshots") // Remove when OneConfig is out of beta
}

dependencies {
    val oneConfigMcVersion = "1.8.9"
    val oneConfigModLoader = "forge"
    val oneconfigVersion = "1.0.0-alpha.XXX" // Put whatever the latest is here
    modImplementation("org.polyfrost.oneconfig:$oneConfigMcVersion-$oneConfigModLoader:$oneConfigVersion")
}
```

{% endtab %}

{% tab title="Groovy" %}

```groovy
repositories {
    maven { url 'https://repo.polyfrost.org/releases' }
    maven { url 'https://repo.polyfrost.org/snapshots' } // Remove when OneConfig is out of beta
}

dependencies {
    def oneConfigMcVersion = "26.1"
    def oneConfigModLoader = "fabric"
    def oneConfigVersion = "1.0.0-alpha.XXX" // Put whatever the latest is here
    modImplementation('org.polyfrost.oneconfig:${oneConfigMcVersion}-${oneConfigModLoader}:${oneConfigVersion}')
}
```

{% endtab %}
{% endtabs %}

