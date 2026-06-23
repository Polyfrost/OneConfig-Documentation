# Callback Events

Getting started with OneConfig's callback-based event system shouldn't be difficult, it's easy to learn and fast. If you've worked with FabricMC or QuiltMC before, you'll already be familiar with how these function.

## Registering a listener & listening for events

Registering a listener is as simple as defining the class of the event you'd like to listen to, and providing a callback to be executed whenever that event is dispatched. This can be done via OneConfig's `EventManager`, like so:

{% tabs %}
{% tab title="Java" %}
```java
public void setupEvents() {
    EventManager.register(TickEvent.Start.class, event -> System.out.println("Tick tick tick!"));
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
fun setupEvents() {
    EventManager.register(TickEvent.Start::class) { event ->
        println("Tick tick tick!")
    }
}
```
{% endtab %}
{% endtabs %}

And that's it! Now, from this example, you'll be listening to `TickEvent.Start`, and every time a new game tick starts, it will print `"Tick tick tick!"` so long as our `setupEvents` method/function is executed at least once in the games' lifetime.

## Kotlin DSL

There is also a Kotlin DSL for an improved developer experience with event listeners:

```kotlin
eventHandler { event: TickEvent.Start ->
    println("Tick tick tick!")
}.register()
```
