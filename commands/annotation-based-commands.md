# Annotation-based Commands

## Understanding how your commands are set up

In order to create a command, you need to annotate a class with the `@Command` annotation and provide it with the data required for users to interact with it (such as a name).

{% tabs %}
{% tab title="Java" %}
```java
@Command({"examplemod", "example", "example_mod"})
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Command(arrayOf("examplemod", "example", "example_mod"))
```
{% endtab %}
{% endtabs %}

The values you provide to the annotation here are what the user types into the chat input to execute your command, such as `/examplemod`

## Executing code when someone runs your command

To start, you'll obviously need to apply your starting annotation on a class, like so:

{% tabs %}
{% tab title="Java" %}
```java
@Command({"examplemod", "example", "example_mod"})
public class ExampleCommand {
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Command(arrayOf("examplemod", "example", "example_mod"))
class ExampleCommand {
}
```
{% endtab %}
{% endtabs %}

From here, you can add your main execution point! This method is executed when the user simply runs your command with no arguments or subcommand, like `/examplemod`

{% tabs %}
{% tab title="Java" %}
```java
@Command({"examplemod", "example", "example_mod"})
public class ExampleCommand {

    @Command
    public void main() {
        System.out.println("Hello, OneConfig!");    
    }

}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Command(arrayOf("examplemod", "example", "example_mod"))
class ExampleCommand {

    @Command
    fun main() {
        println("Hello, OneConfig!");    
    }

}
```
{% endtab %}
{% endtabs %}

When the user executes any of the provided command names, "Hello, OneConfig!" will be printed out to the console / log file.

## Command parameters

Now that you know how to create your command, and allow users to run it on it's own, let's take a look at allowing the user to input data.

Let's say we want to take in a name to greet someone in the console. We'd need the user to provide a string.

{% tabs %}
{% tab title="Java" %}
```java
@Command({"examplemod", "example", "example_mod"})
public class ExampleCommand {

    @Command
    public void main(@Parameter("Name") @NotNull String name) {
        System.out.println("Hello, " + name + "!");    
    }

}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Command(arrayOf("examplemod", "example", "example_mod"))
class ExampleCommand {

    @Command
    fun main(@Parameter("Name") name: String) {
        println("Hello, $name!");    
    }

}
```
{% endtab %}
{% endtabs %}

In the above example, we take a non-optional parameter called "Name", which we can then use to print out a greeting in the console.

### Parameter parsers

OneConfig provides default parsers for all of the basic primitive types and very few custom types, such as Minecraft's `GameProfile`, meaning that you'll need to provide your own parser for your own data objects.

So, let's say we have en enum type:

```java
public enum ExampleEnum {
    LOREM,
    IPSUM
}
```

And we want the user to be able to select one of it's values. For this, we will need to create a custom `ArgumentParser`.

{% tabs %}
{% tab title="Java" %}
```java
public class ExampleEnumArgumentParser extends ArgumentParser<ExampleEnum> {
    
    @Override
    public ExampleEnum parse(@NotNull String arg) {
        return ExampleEnum.valueOf(arg.toUpperCase(Locale.US));
    }
    
    @Override
    public @Nullable List<String> getAutoCompletions(String arg) {
        if (arg.isEmpty()) {
            return null;
        }
        
        List<String> result = new ArrayList<>();
        for (ExampleEnum value : ExampleEnum.values()) {
            String name = value.name().toLowerCase(Locale.US);
            if (!name.startsWith(arg.toLowerCase(Locale.US))) {
                continue;
            }
            
            result.add(name);
        }
        
        return result;
    }
    
    @Override
    public Class<ExampleEnum> getType() {
        return ExampleEnum.class;
    }
    
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
class ExampleEnumArgumentParser : ArgumentParser<ExampleEnum>() {
    
    override fun parse(arg: String): ExampleEnum {
        return ExampleEnum.valueOf(arg.toUpperCase(Locale.US))
    }
    
    override fun getAutoCompletions(arg: String): List<String>? {
        if (arg.isEmpty()) {
            return null
        }
        
        val result = mutableListOf<String>()
        for (value in ExampleEnum.values()) {
            String name = value.name().toLowerCase(Locale.US)
            if (!name.startsWith(arg.toLowerCase(Locale.US))) {
                continue
            }
            
            result.add(name)
        }
        
        return result
    }
    
    override fun getType(): Class<ExampleEnum> {
        return ExampleEnum::class.java;
    }
    
}
```
{% endtab %}
{% endtabs %}

So... What's going on here?!

First, in our `parse` method, we're taking our `arg` value and converting it to full uppercase to conform to enum naming conventions, then trying to find a value matching that name inside of `ExampleEnum`.

Then, we implement autocompletion in `getAutoCompletions` by checking the current input against all possible values in the enum. **This is entirely optional**, we can simply return null to opt out of autocomplete for whatever reason.

Lastly, we provide our `ArgumentParser` with the definitive type of our custom object so that OneConfig's internals can determine when and where our parser needs to be utilized.

Now, when we create a command with `ExampleEnum` as one of the parameter types, a user will be able to input any of the names in our enum and our command's execution point will receive that enum! Nifty, huh?

## Subcommands

When you've got multiple functions under a single base command name, you're going to want to separate them into multiple subcommands. Luckily, it's as easy as creating more methods and annotating them with the very same annotation you used to create your base command:

{% tabs %}
{% tab title="Java" %}
```java
@Command({"examplemod", "example", "example_mod"})
public class ExampleCommand {

    @Command({"greet", "grt"})
    public void greet(@Parameter("Name") @NotNull String name) {
        System.out.println("Hello, " + name + "!");    
    }

}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Command(arrayOf("examplemod", "example", "example_mod"))
class ExampleCommand {

    @Command(arrayOf("greet", "grt"))
    fun greet(@Parameter("Name") name: String) {
        println("Hello, $name!");
    }

}
```
{% endtab %}
{% endtabs %}

Now, instead of your users needing to type `/examplemod <NAME>` in the chat to greet someone in their console, they will be required to type `/examplemod greet <NAME>` or `/examplemod grt <NAME>`, as define by our subcommand.

