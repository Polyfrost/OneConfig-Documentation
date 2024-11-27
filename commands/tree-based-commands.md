# Tree-based Commands

To get started with OneConfig's tree-based ([Brigadier](https://github.com/Mojang/Brigadier)-style) command system, you'll need to get started by creating a `CommandBuilder:`

{% tabs %}
{% tab title="Java" %}
```java
CommandBuilder builder = CommandBuilder.command("examplemod", "example", "example_mod");
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val builder = CommandBuilder.command("examplemod", "example", "example_mod")
```
{% endtab %}
{% endtabs %}

From here, if you want to do something when the command is run on it's own (f.ex `/examplemod`), you can use the `runs` method to define what is executed, like so:

{% tabs %}
{% tab title="Java" %}
```java
builder.then(CommandBuilder.runs().does(() -> {
    System.out.println("Hello, OneConfig!");
}));
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
builder.then(CommandBuilder.runs().does {
    println("Hello, OneConfig!")
})
```
{% endtab %}
{% endtabs %}

Both the object which `command` and `runs` returns have a `description` method which allow you to describe what happens when you execute that command or subcommand, it is recommended to use this where possible.

Finally, to register your command, you can simply use `CommandManager#registerCommand` like so:

{% tabs %}
{% tab title="Java" %}
```java
CommandManager.registerCommand(builder.build());
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
CommandManager.registerCommand(builder.build())
```
{% endtab %}
{% endtabs %}

