# Migrating your configs from Vigilance

## Updating from V0

OneConfig V0 had a system in which you would add a `new VigilanceMigrator(...)` to your config's super constructor call in order to tell it where to find your old Vigilance config. Now, in OneConfig V1, we are prioritizing allowing developers to migrate from more other config systems independently.

You can now replace your `VigilanceMigrator` instantiation with a call to `loadFrom` in your constructor, passing the path to your old config to it.

You can also replace all `@VigilanceName` annotations with the new `@PreviousNames` annotation, in which you can simply pass the full path (category + subcategory + name) to your old option, f.ex: `"oldCategory.oldSubcategory.oldName1", "oldCategory.oldName2", ...`

## Full example

{% tabs %}
{% tab title="Java" %}
```java
public class MyConfig extends Config {

    @Switch(
        title = "My Switch",
        description = "This is my switch",
        icon = "/my_switch.svg",
        category = "Switches",
        subcategory = "General"
    )
    @PreviousNames({"switches.general.mySwitch"})
    public static boolean mySwitch = false;
    
    public MyConfig() {
        super(
              "example_config.json",
              "/assets/examplemod/example_mod.png",
              "Example Mod",
              Category.QOL
         );
    
        loadFrom("config/my_mod.toml"); // Old Vigilance config
    }

}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
object MyConfig : KtConfig(
     id = "example_config.json",
     icon = "/assets/examplemod/example_mod.png",
     title = "Example Mod",
     category = Config.Category.QOL
) {

    // TODO: Add @PreviousNames annotation for the Kotlin DSL
    var mySwitch: Boolean by switch(
        name = "My Switch",
        def = false, // Sets option's default value. Recommended, default = true
        description = "This is my switch", // Recommended, default = ""
        icon = "/my_switch.svg", // Optional, default = ""
        category = "Switches", // Recommended, default = "General"
        subcategory = "General" // Recommended, default = "General"
    )
    
    init {
        loadFrom("config/my_mod.toml") // Old Vigilance config
    }

}
```
{% endtab %}
{% endtabs %}
