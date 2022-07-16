---
description: Learn how to migrate configs to OneConfig.
---

# Migration

You might want to migrate a different config to OneConfig so users don't lose their configs, OneConfig has the ability to do that.

OneConfig includes a migrator for vigilance, but you can also create a custom migrator if you need that.

### Vigilance Migrator

To use the vigilance migrator all you need to do is register it and give it the location to your old vigilance config.

```java
public MyConfig() {
    super(new Mod("My Mod", ModType.UTIL_QOL, new VigilanceMigrator("./old-config.toml")), "config.json");
    initialize();
}
```

If you change the name of an option or what category or subcategory the option is in you will have to provide the old values so the option can be migrated properly, you can do this like this.

```java
@Switch(
    name = "A random switch",
    category = "General",
    subcategory = "Switches"
)
@VigilanceName(
    name = "Old Name",
    category = "Old Category",
    subcategory = "Old Subcategory"
)
public static boolean bob = false;
```

### Custom Migrator

To create a custom migrator you have to implement the `Migrator` interface and implement the `getValue` function, this function returns the value the field should be set too. For a full example see [`VigilanceMigrator`](https://github.com/Polyfrost/OneConfig/blob/master/src/main/java/cc/polyfrost/oneconfig/config/migration/VigilanceMigrator.java).

```java
public class MyMigrator implements Migrator {
    @Override
    public Object getValue(Field field, String name, String category, String subcategory) {
        // logic to get old value and return object here
    }
}
```

Then to use this migrator just define it when you create your config like the vigilance migrator.

```java
public MyConfig() {
    super(new Mod("My Mod", ModType.UTIL_QOL, new MyMigrator()), "config.json");
    initialize();
}
```
