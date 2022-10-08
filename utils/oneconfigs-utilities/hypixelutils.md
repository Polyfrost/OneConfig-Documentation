---
description: A more detailed look into the HypixelUtils that OneConfig has
---

# HypixelUtils

OneConfig has a collection of Hypixel-orientated utilities, most notably for the locraw system that Hypixel offers. Credit to [Seraph](https://github.com/Scherso/Seraph) for allowing us to include it in OneConfig!

These utilities work by sending the `/locraw` command when the client is detected to be on the Hypixel server. This then allows you to get various information on what server, what map, and what gamemode the player is in.



### LocrawInfo <a href="#locraw" id="locraw"></a>

LocrawInfo is the name of the class given to the information gathered from the locraw message. It contains the following information:

* Server ID, e.g. mini121
* Gamemode, for example eight\_two for Doubles BedWars
* Game type, for example SKYWARS for SkyWars
* Map name, such as Shire
