---
description: Learn more about the Packet events OneConfig has to offer
---

# Packet Events

## SendPacketEvent

SendPacketEvent is (as the name suggests) an event that is fired every time the client sends a packet.

This event also gets the packet that is going to be sent, as a `Packet<?>`. You can use code like the code below to do things with it.

{% hint style="warning" %}
This event is cancellable, meaning you can stop the packet from getting into the games code. Be careful with what you cancel!
{% endhint %}

```java
@Subscribe
public void onPacketSend(SendPacketEvent event) {
    // check if the packet is the right type
    if(event.packet instanceof C14PacketTabComplete) {
        // cast the packet to the right type
        C14PacketTabComplete packet = (C14PacketTabComplete) event.packet;
        // do something with it
        System.out.println("Attempted to send a tab complete packet with message:" + packet.getMessage());
        // cancel the event afterwards, rendering this packet useless.
        event.isCancelled = true;
    }
}
```

## ReceivePacketEvent

ReceivePacketEvent is (as the name suggests) an event that is fired every time the client receives a packet.

This event also gets the packet that has been received, as a `Packet<?>`. You can use code like the code below to do things with it.

{% hint style="warning" %}
This event is Cancel-able, meaning you can stop the packet from getting into the games code. Be careful with what you cancel!
{% endhint %}

```java
@Subscribe
public void onPacketReceive(ReceivePacketEvent event) {
    // check if the packet is the right type
    if(event.packet instanceof S0FPacketSpawnMob) {
        // cast the packet to the right type
        S0FPacketSpawnMob packet = (S0FPacketSpawnMob) event.packet;
        // do something with it
        System.out.println("Received data from server about an entity spawned with ID: " + packet.getEntityID());
    }
}
```
