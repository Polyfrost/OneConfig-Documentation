---
description: Find out how to create Configs with OneConfig
---

# Creating a Config

## Getting Started

### Building the bare bones

To create a new config, you need to create a new class that extends `Config`, just like this:

```java
public class MyConfig extends Config {
}
```

Simple! Now, it needs a constructor. The `Mod` object stores both its name and category, along with the mod's file name. Usually, named `"yourmodname.json"`.

```java
public MyConfig() {
    // Available mod types: PVP, HUD, UTIL_QOL, HYPIXEL, SKYBLOCK
    super(new Mod("My Mod", ModType.UTIL_QOL), "config.json");
    initialize();
}
```

### Additional cosmetics

If you wish, you can specify an icon for your mod that will be shown in the GUI. All you need to do is add a third argument that specifies your icon's file path.

```java
public MyConfig() {
    // Available mod types: PVP, HUD, UTIL_QOL, HYPIXEL, SKYBLOCK
    super(new Mod("My Mod", ModType.UTIL_QOL, "/filepath/to/icon.png"), "config.json");
    initialize();
}
```

{% hint style="info" %}
OneConfig supports both the PNG and SVG (vector) image formats.
{% endhint %}

## Initializing on launch

Finally, you have to initialize your config when the game launches. This can easily be done using the [Broken link](broken-reference "mention") system, with the `InitializationEvent`, most commonly in your main class:

```java
public class MyMod {
    public static MyConfig config;

    @SubscribeEvent
    public void onInit(InitializationEvent event) {
        config = new MyConfig();
    }
}
```

And you're done, pretty simple huh? Your config is now registered and can be seen in the GUI. So naturally, it's time to add some options.

{% content-ref url="adding-options/" %}
[adding-options](adding-options/)
{% endcontent-ref %}



## Example Config GUI

Here is an example config GUI, if you are looking for a sneak peek or some inspiration :)

![Example Config GUI for inspiration](<../.gitbook/assets/image (6).png>)
