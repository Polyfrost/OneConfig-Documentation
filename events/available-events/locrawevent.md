---
description: Learn more about LocrawEvent
---

# LocrawEvent

## What is Locraw?

Locraw is a Hypixel specific feature which means Location Raw, and it is a .json String sent by the server to the chat upon typing of the command /locraw. It is extremely useful for mods that are gamemode-specific, for example Skyblock mods that should only work in Skyblock. See [hypixelutils.md](../../utils/available-utilities/hypixelutils.md "mention") for more information on Locraw.

## Event information

LocrawEvent is fired every time a Locraw message is received from the server successfully. It is intended as another method to get the location of the player, besides checking the fields of the HypixelUtils class.

Here is some code demonstrating its features:

```java
@Subscribe
public void onLocraw(LocrawEvent event) {
    // print out the location of the player
    System.out.println("got location: " + event.info.toString());
    if(event.info.gameType == LocrawInfo.GameType.BEDWARS) {
        System.out.println("in bedwars game!");
    }
}
```
