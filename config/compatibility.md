---
description: Learn how to migrate configs to OneConfig.
---

# Migration

### What are they?

OneConfig includes a migration system, which can be used to turn various forms of old config files or other config systems into OneConfig readable ones. OneConfig has built-in support for JSON files, Vigilance, and .cfg Forge files.

These Migrators are extremely useful for if you are wanting to change from using a different config system to the OneConfig one, as it allows your users to just update the mod and their config should be automatically migrated into the OneConfig system!

All migrators implement the Migrator interface, and you can create your own as well if you want. They all work in the same way, where you pass the expected location on the player's client to the old config file, and OneConfig will do the rest, like this:

```java
public MyConfig() {
    super(new Mod("My Mod", ModType.UTIL_QOL, new VigilanceMigrator("./old-config.toml")), "config.json");
    initialize();
}
```

### MigrationNames

Sometimes, you might want to change the name of a field or config element in the new OneConfig system. Don't worry though! We've thought of that and created various `@Annotations` for you to use to ensure that OneConfig can find the old field in the file.

Here is an example of a VigilanceName:

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

To create a custom migrator, you have to implement the `Migrator` interface and implement the `getValue` function, and this function returns the value the field should be set too, according to the old config. For a full example see [`VigilanceMigrator`](https://github.com/Polyfrost/OneConfig/blob/master/src/main/java/cc/polyfrost/oneconfig/config/migration/VigilanceMigrator.java).

```java
public class MyMigrator implements Migrator {
    @Override
    public Object getValue(Field field, String name, String category, String subcategory) {
        // logic to get old value and return object here
    }
}
```
