---
description: Learn how to migrate configs to OneConfig.
---

# Migration

### What is this?

OneConfig includes a system to help you migrate configs into ones OneConfig can use. For example, OneConfig has built-in support for; JSON, Vigilance, and .cfg Forge files. This is very useful if you want to seamlessly migrate your old mods to OneConfig.

All migrators implement the Migrator interface, and you can create your own as well if you want. They all work in the same way, where you pass the expected location on the player's client to the old config file, and OneConfig will do the rest, like this:

```java
public MyConfig() {
    super(new Mod("My Mod", ModType.UTIL_QOL, new VigilanceMigrator("./old-config.toml")), "config.json");
    initialize();
}
```

### MigrationNames

Maybe you want to change the name of an old field or element in the new system. We've thought of this, and you can use our various `@Annotations` to maintain the support of your old files. See an example below, using Vigilance.&#x20;

```java
@VigilanceName(                    // retrieve the value from the old JSON file  
    name = "Old Name",
    category = "Old Category",
    subcategory = "Old Subcategory"
)
@Switch(                           // initialize a field like a normal config  
    name = "A random switch",
    category = "General",
    subcategory = "Switches"
)
public static boolean bob = false;
```

And a JsonName:

```java
 @JsonName("hearts.blur.disabled")                     // retrieve the value from the old JSON file  
 @Switch(name = "Disable Blur", category = "Hearts")   // initialize a field like a normal config  
 public static boolean isHeartsBlurDisabled = false;
```



### Custom Migrators

To create a custom migrator, you have to implement the `Migrator` interface and implement the `getValue` function, and this function returns the value the field should be set to, according to the old config. For a full example see [`VigilanceMigrator`](https://github.com/Polyfrost/OneConfig/blob/master/src/main/java/cc/polyfrost/oneconfig/config/migration/VigilanceMigrator.java).

```java
public class MyMigrator implements Migrator {
    @Override
    public Object getValue(Field field, String name, String category, String subcategory) {
        // logic to get old value and return object here
    }
}
```
