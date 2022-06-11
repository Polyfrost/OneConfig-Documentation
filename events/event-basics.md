---
description: Learn more about Events, how they work and their purpose
---

# Event Basics

If you are familiar with Java libraries like `javax.swing`, or have done Forge/Fabric coding before, then don't worry - events shouldn't be a mystery to you!

Forge and Fabric already use events, however they are not very multiplatform - they change massively version to version. That's why OneConfig has its own event system, helping OneConfig to achieve its aim of uniting all Minecraft mods.

## Getting on the Bus

To get events to work, its important to register any Object/Class that uses them to the EventBus. This is very simple, and its a great idea to do this in your constructor, for example:

```java
public MyClassConstructor() {
    EventManager.INSTANCE.register(this);
}
```

This will allow that class to use the Event system. Continue reading to subscribe to your first event!

## Using the Bus

Once you have registered your class, you can now `@Subscribe` to (use) the events you would like. For example, to subscribe to a TickEvent:

```java
@Subscribe
private void onTick(TickEvent event) { // the parameter type specifies what event you are subscribing to
    // do something every tick (once every 50ms in Minecraft)
}
```

{% hint style="danger" %}
All methods annotated with `@Subscribe` must not be static!
{% endhint %}

So, as a general rule for events:

* [ ] Subscribe your class to the EventBus using EventManager
* [ ] Annotate your method you would like to use an event using `@Subscribe`
* [ ] Choose your event type by setting the parameter type in the method (you can name the variable whatever you want, a common name is just `event`)

Easy as that!
