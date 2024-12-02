# Creating Your Config

## Getting Started

### Building your base

To create your config, you'll first need to create a new class that extends OneConfig's `Config` class, like so:

{% tabs %}
{% tab title="Java" %}
```java
public class ExampleConfig extends Config {
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
object ExampleConfig : KtConfig() // This is an object so we can easily access a singleton instance of the config. Refer to later section for more info
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
### Why do we use KtConfig for the Kotlin example?

KtConfig provides additional functionality which makes it easier to create type-safe options in Kotlin with a much more readable and serviceable syntax.
{% endhint %}

Easy, right? Now, you'll need to provide it with some info via it's **constructor**, which takes your config's name, category, file name and some other relating data.

The filename you pass to OneConfig is what the file will be named inside of the user's OneConfig settings profile, f.ex `.minecraft/config/OneConfig/profiles/example_config.json`.

{% tabs %}
{% tab title="Java" %}
```java
public class ExampleConfig extends Config {
    public ExampleConfig() {
         super(
              "example_config.json",                // Your mod's config file's name and extension
              "/assets/examplemod/example_mod.png", // A path to a PNG or SVG file, used as your mod's icon in OneConfig's UI
              "Example Mod",                        // Your mod's name was it is shown in OneConfig's UI
              Category.QOL                          // The category your mod will be sorted in within OneConfig's UI
         );
    }
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
object ExampleConfig : KtConfig(
     id = "example_config.json",                  // Your mod's config file's name and extension
     icon = "/assets/examplemod/example_mod.png", // A path to a PNG or SVG file, used as your mod's icon in OneConfig's UI
     title = "Example Mod",                       // Your mod's name was it is shown in OneConfig's UI
     category = Config.Category.QOL               // The category your mod will be sorted in within OneConfig's UI
)
```
{% endtab %}
{% endtabs %}

Simple as that!&#x20;

## Initializing your config when the game launches

There are various different ways to initialize your config, but here are the way we recommend:

If you are on **Java**, add an `INSTANCE` field to your config. This is where you will access your dedicated object of your config for non-static methods, such as `save`.

```java
public class ExampleConfig extends Config {

    // Your actual config options here...
    
    public static final ExampleConfig INSTANCE = new ExampleConfig();
    
    // Your constructor here...
}
```

If you are on **Kotlin** and you have not already, make your config class an `object`. This makes your class a singleton, which essentially will create the `INSTANCE` field in Java for you, and make accessing it via Kotlin syntax easier.

```kotlin
object ExampleConfig : KtConfig(
     // Your constructor stuff here...
)
```

Now, all you need to do is initialize your config when the game first launches with your mod, via the `preload` method. This can be done using your mod loader's standard means of initializing your mod at game launch, or alternatively, by using OneConfig's events system, using the `InitializationEvent`.

{% tabs %}
{% tab title="Java (Forge 1.8.9)" %}
```java
@Mod(modid = ExampleMod.MODID, version = ExampleMod.VERSION, name = ExampleMod.NAME)
public class ExampleMod {
    public static final String MODID = "examplemod";
    public static final String VERSION = "1.0.0";
    public static final String NAME = "Example Mod";
    
    @Mod.EventHandler
    public void onInitialize(FMLInitializationEvent event) {
        ExampleConfig.INSTANCE.preload();  // Ensures that everything is set up as it should be!
    }
}
```
{% endtab %}

{% tab title="Kotlin (Forge 1.8.9)" %}
```kotlin
@Mod(modid = ExampleMod.MODID, version = ExampleMod.VERSION, name = ExampleMod.NAME)
class ExampleMod { // This can also be an object via a language adapter, which you can use via OneConfig!
    companion object {
        const val MODID = "examplemod"
        const val VERSION = "1.0.0"
        const val NAME = "Example Mod"
    }
    
    @Mod.EventHandler
    fun onInitialize(event: FMLInitializationEvent) {
        // Unlike Java, you don't need the `INSTANCE` reference here.
        ExampleMod.preload() // Ensures that everything is set up as it should be!
    }
}
```
{% endtab %}

{% tab title="Java (OneConfig Events)" %}
```java
public class ExampleMod {
    
    @Subscribe
    public void onInitialize(InitializationEvent event) {
        ExampleConfig.INSTANCE.preload();  // Ensures that everything is set up as it should be!
    }
}
```
{% endtab %}

{% tab title="Kotlin (OneConfig Events)" %}
```kotlin
class ExampleMod {
    
    @Subscribe
    fun onInitialize(event: InitializationEvent) {
        // Unlike Java, you don't need the `INSTANCE` reference here.
        ExampleConfig.preload()  // Ensures that everything is set up as it should be!
    }
}
```
{% endtab %}
{% endtabs %}
