---
description: Learn more about HudRenderEvent
---

# HudRenderEvent

HudRenderEvent is an event that is fired when the GameOverlay for Minecraft is rendered (things like the hotbar, sidebar, etc.)



You can use `deltaTicks` to access the time elapsed since the last tick occurred, which is useful for animations.

```java
@Subscribe
public void onHudRender(HudRenderEvent event) {
    RenderManager.setupAndDraw((vg) -> {
        // draw a rounded rectangle on the screen
        RenderManager.drawRoundedRect(vg, 10, 50, 100, 100, -1, 12f);
    }
}
```
