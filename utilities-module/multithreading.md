# Multithreading

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
```kotlin
val action = Runnable {
    println("Hello! I'm in another thread!")
}

Multithreading.submit(action)
```
{% endtab %}
{% endtabs %}

## Scheduling an action to run after some time

{% tabs %}
{% tab title="Java" %}
<pre class="language-java"><code class="lang-java"><strong>Runnable action = () -> {
</strong>    System.out.println("Hello! I'm in another thread and was run after 5 seconds!");
};
<strong>
</strong><strong>Mulithreading.schedule(action, 5, TimeUnit.SECONDS);
</strong></code></pre>
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val action = Runnable {
    println("Hello! I'm in another thread and was run after 5 seconds!")
}

Mulithreading.schedule(action, 5, TimeUnit.SECONDS)
```
{% endtab %}
{% endtabs %}
