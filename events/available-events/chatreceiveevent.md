---
description: Learn more about ChatReceiveEvent
---

# ChatReceiveEvent

ChatReceiveEvent is an event that is fired when the client receives a chat message.

{% hint style="warning" %}
This event is Cancellable, meaning you can stop other mods and the game itself from receiving messages. Be careful!
{% endhint %}

You can use `event.message` to get the message that was received as a `IChatComponent`. If you want it as plain text, don't worry! You can use `.getUnformattedText()` to get the message as a plain String.

```java
@Subscribe
public void onChatReceive(ChatReceiveEvent event) {
    System.out.println("I just received a message! " + event.message.getUnformattedText());
}
```
