# Using the events system

OneConfig has it's own custom event system, which can either be callback- or subscriber-based depending on your preferences. It provides several default events relating to basic OneConfig functionality and Minecraft-relating functionality.

If you have used the [Fabric API](https://modrinth.com/mod/fabric-api/), you are likely more familiar with **callback-based events**.\
If you have worked with [MinecraftForge](https://files.minecraftforge.net/net/minecraftforge/forge/) or [NeoForge](https://neoforged.net/), you are likely more familiar with **subscriber-based events**.

It is preferred to use callback-based events for code quality, maintainability and speed.

{% content-ref url="callback-events.md" %}
[callback-events.md](callback-events.md)
{% endcontent-ref %}

{% content-ref url="subscriber-events.md" %}
[subscriber-events.md](subscriber-events.md)
{% endcontent-ref %}

