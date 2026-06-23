# Tree-based Commands

OneConfig uses the Minecraft command system ([Brigadier](https://github.com/Mojang/Brigadier)) for non annotation based commands, however it provides some utility functions.

You can create a simple command like the following.

{% tabs %}
{% tab title="Java" %}
```java
var builder = CommandManager.literal("examplemod");
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val builder = CommandManager.literal("examplemod")
```
{% endtab %}
{% endtabs %}

From here, if you want to do something when the command is run on it's own (f.ex `/examplemod`), you can use the `executes` method to define what is executed, like so:

{% tabs %}
{% tab title="Java" %}
```java
builder.executes(ctx -> {
    System.out.println("Hello, OneConfig!"); 
    
    return Command.SINGLE_SUCCESS;
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
builder.executes { ctx ->
    println("Hello, OneConfig!")
    
    Command.SINGLE_SUCCESS
}
```
{% endtab %}
{% endtabs %}

Finally, to register your command, you can simply use `CommandManager.register` like so:

{% tabs %}
{% tab title="Java" %}
```java
CommandManager.register(builder);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
CommandManager.register(builder)
```
{% endtab %}
{% endtabs %}

For a more detailed documentation of Brigadier, and it's API you can check out following resources:
- [Creating Commands | Fabric Docs](https://docs.fabricmc.net/develop/commands/basics)
- [Readme | Brigadier Repository](https://github.com/Mojang/Brigadier)