---
description: Learn more about the TickEvent
---

# TickEvent

TickEvent is an event that is fired twice Minecraft tick - once at the start, and once at the end. Minecraft ticks happen once every 50ms, or 20 times per second.

You can specify when you want this to be fired using `Stage`, like this:

```java
@Subscribe
public void onTick(TickEvent event) {
    if(event.stage == Stage.START) {
        // do something at the start of the tick
    }
    if(event.stage == Stage.END) {
        // do something at the end of the tick.
    }
}
```

If the Stage of the event is not checked, your code may run twice. Be careful!
