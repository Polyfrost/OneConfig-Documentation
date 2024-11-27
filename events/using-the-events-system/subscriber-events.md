# Subscriber Events

Getting started with OneConfig's subscriber-based events system is easy and straightforward! If you've worked with MinecraftForge or NeoForge before, you'll be more than familiar with how these function.

## Registering a listener

In order for your subscriber methods to execute when an event is dispatched, you'll need to register their containing instance as an event listener. This can be done via an instance of `EventManager`, typically the statically provided `INSTANCE`:

{% tabs %}
{% tab title="Java" %}
```java
public class ExampleListener {
    // This should be called somewhere - Like when your mod is first initialized
    public void run() {
        EventManager.INSTANCE.register(this);
    }
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
object ExampleListener {
    // This should be called somewhere - Like when your mod is first initialized
    fun run() {
        EventManager.INSTANCE.register(this)
    }
}
```
{% endtab %}
{% endtabs %}

## Listening for events

Now that your instance is registered as an event listener, you can define your subscriber methods for the events which you want to listen for dispatches of. This can be done by defining those events as parameters for a method/function then annotating that same method/function with `@Subscribe`.

{% tabs %}
{% tab title="Java" %}
```java
public class ExampleListener {
    // This should be called somewhere - Like when your mod is first initialized
    public void run() {
        EventManager.INSTANCE.register(this);
    }
    
    // This method is called every tick, as the TickEvent is dispatched every game tick
    @Subscribe
    public void onTick(TickEvent.Start event) { // TickEvent.End also exists.
        System.out.println("Tick tick tick!");   
    }
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
object ExampleListener {
    // This should be called somewhere - Like when your mod is first initialized
    fun run() {
        EventManager.INSTANCE.register(this)
    }
    
    // This method is called every tick, as the TickEvent is dispatched every game tick
    @Subscribe
    fun onTick(event: TickEvent) {
        println("Tick tick tick!")
    }
}
```
{% endtab %}
{% endtabs %}

And there you have it! This instance of our `ExampleListener` now receives all dispatched instances of `TickEvent.Start` as long as our `run` method/function is executed at least once in it's lifetime.
