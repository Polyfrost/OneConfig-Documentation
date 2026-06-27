# Listening For Option Changes

Monitoring changes to options for any reason is simple, thanks to the convenient methods provided by OneConfig. You can use them like so:

{% tabs %}
{% tab title="Java" %}
```java
public MyConfig() {
    addCallback("myOptionName", () -> {
        System.out.println("myOptionName changed!");
    });
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val myOptionName by observable(switch(<...>)) {
    println("myOptionName changed!")
}

val myOptionName by switch(<...>).onChange { println("myOptionName changed!") }
```
{% endtab %}
{% endtabs %}

Easy enough, eh? But what if we want to know the new value at the time of the change?

{% tabs %}
{% tab title="Java" %}
```java
public MyConfig() {
    addCallback<Boolean>("myOptionName", (value) -> {
        System.out.println("myOptionName value: " + value);
    });
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val myOptionName by observable(switch(<...>)) {
    println("myOptionName value: $it")
}

val myOptionName by switch(<...>).onChange { println("myOptionName value: $it") }
```
{% endtab %}
{% endtabs %}
