---
description: Learn more about InitializationEvent
---

# InitializationEvent

InitializationEvent is an event that is fired when the client launches. It is the same as `FMLInitializationEvent` if you are a forge coder.&#x20;

If you are using OneConfig's configuration system, its a great place to initialize your config as well:

```java
@Subscribe
public void init(InitializationEvent event) {
    System.out.println("The game is starting!");
    config = new MyConfig();    // initialize your config 
}
```
