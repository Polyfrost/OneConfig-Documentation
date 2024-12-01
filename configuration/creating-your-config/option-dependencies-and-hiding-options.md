# Option Dependencies & Hiding Options

## Dependency management

{% tabs %}
{% tab title="Java" %}
```java
public MyConfig() {
    addDependency("myOptionName", "myOtherOptionName"); // Disables myOptionName when myOtherOptionName = false
    // The above obviously only works when myOtherOptionName is a boolean-typed option.
    
    addDependency("myOtherOtherOptionName", () -> Property.Display.HIDDEN); // Hides myOtherOtherOptionName
    
    addDependency("myOtherOtherOtherOptionName", "myOptionName", true); // Hides myOtherOtherOtherOptionName when myOptionName is false
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
init {
    addDependency("myOptionName", "myOtherOptionName") // Disables myOptionName when myOtherOptionName = false
    // The above obviously only works when myOtherOptionName is a boolean-typed option.
    
    addDependency("myOtherOtherOptionName") { Property.Display.HIDDEN } // Hides myOtherOtherOptionName
    
    addDependency("myOtherOtherOtherOptionName", "myOptionName", true) // Hides myOtherOtherOtherOptionName when myOptionName is false
}
```
{% endtab %}
{% endtabs %}

## Hiding your options

{% tabs %}
{% tab title="Java" %}
```java
public MyConfig() {
    hideIf("myOptionName", () -> true); // Hides myOptionName
    
    hideIf("myOptionName", "myOtherOptionName"); // Hides myOptionName if myOtherOptionName is false
    // The above obviously only works when myOtherOptionName is a boolean-typed option.
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
init {
    hideIf("myOptionName") { true } // Hides myOptionName
    
    hideIf("myOptionName", "myOtherOptionName") // Hides myOptionName if myOtherOptionName is false
    // The above obviously only works when myOtherOptionName is a boolean-typed option.
}
```
{% endtab %}
{% endtabs %}

## What's the difference?

You can use `addDependency` to fine-tune the display status of your options based on your own conditions or other options. By default, simply using `addDependency` and passing the options of your choosing will cause the dependant to be disabled rather than hidden.

`hideIf` will ALWAYS completely hide the option passed to it based on the condition(s) provided as opposed to having to pick a display status.
