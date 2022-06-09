---
description: OneConfig's easy to use, multiplatform GuiScreen alternative
---

# OneUIScreen

## Why?

OneUIScreen exists for one primary reason: Multiplatform.

Changes between loaders, mappings and versions are notoriously bad in Minecraft, so that is why we created OneUIScreen: It's the same for every version of Minecraft.

OneUIScreen also exists because we wanted a GUI Screen that had native NanoVG support: There is no need for `RenderManager.setupAndDraw`, and you can just get going straight away.&#x20;

It also has parity between the names of methods, and includes much stronger and more robust mouse input handling (see [inpututils.md](../utils/available-utilities/inpututils.md "mention") for more information on that).

## Creating a OneUIScreen

Creating a OneUIScreen is simple - just extend the class, like so:

```java
public class MyScreen extends OneUIScreen {
    public MyScreen() {
        super();        // constructor for your screen - you can initialize things here as well
    }
    
    public void onScreenOpen() {
        // setup variables, initialze components, etc.
    }
    
    public void draw(long vg, float partialTicks) {
        // draw script for the screen with a NanoVG context already prepared
        RenderManager.drawRoundedRect(10,50,100,100,-1,12f);
        // You can also use partialTicks for animations as a deltaTime.
    
    public void onScreenClose() {
        // clean up, etc. when the screen closes.
    }
```

## Displaying Your Screen

You can Display your screen in many ways, for example using a [Broken link](broken-reference "mention") implementation, or opening it when a key is pressed using [onekeybind.md](../utils/onekeybind.md "mention"). They can be opened easily using `GuiUtils.displayScreen(new MyScreen())`.&#x20;
