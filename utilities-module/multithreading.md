# Multithreading

OneConfig comes with a builtin util to make async executing, and delayed async running more convenient.

## Submitting actions to run in multiple threads

{% tabs %}
{% tab title="Java" %}
```java
Runnable action = () -> {
    System.out.println("Hello! I'm in another thread!");
};

Multithreading.submit(action);
```
{% endtab %}

{% tab title="Kotlin" %}

In kotlin you can either use the Java API
```kotlin
val action = Runnable {
    println("Hello! I'm in another thread!")
}

Multithreading.submit(action)
```
Or by using the kotlin helper function

```kotlin
submit {
    println("Hello! I'm in another thread!")
}
```
{% endtab %}
{% endtabs %}

## Scheduling an action to run after some time

{% tabs %}
{% tab title="Java" %}
```java
Runnable action = () -> {
    System.out.println("Hello! I'm in another thread and ran after 5 seconds!");
};

Mulithreading.schedule(action, 5, TimeUnit.SECONDS);
```
{% endtab %}

{% tab title="Kotlin" %}

In kotlin you can either use the Java API
```kotlin
val action = Runnable {
    println("Hello! I'm in another thread and ran after 5 seconds!")
}

Mulithreading.schedule(action, 5, TimeUnit.SECONDS)
```

Or using one of the kotlin helper function

```kotlin
schedule(5, TimeUnit.SECONDS) {
    TODO("<...>")
}

schedule(5.seconds) {
    TODO("<...>")
}
```
{% endtab %}
{% endtabs %}
