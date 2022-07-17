---
description: OneConfig's easy to use, multiplatform GuiScreen alternative
---

# OneUIScreen

## Why?

OneUIScreen is a convenient class that can be used for easy handling of mouse, keyboard, and rendering with NanoVG (see [inpututils.md](../utils/available-utilities/inpututils.md "mention")).

## Creating a OneUIScreen

Creating a OneUIScreen is simple - just extend the class, like so:

```java
public class MyScreen extends OneUIScreen {
    public MyScreen() {
        super();        // constructor for your screen - you can initialize things here as well
    }

    @Override
    public void initScreen(int width, int height) {
        super.initScreen(width, height);
        // setup variables, initialize components, etc.
    }       

    @Override
    public void draw(long vg, float partialTicks) {
        // draw script for the screen with a NanoVG context already prepared
        RenderManager.drawRoundedRect(10,50,100,100,-1,12f);
        // You can also use partialTicks for animations as a deltaTime.

    @Override
    public void onScreenClose() {
        // clean up, etc. when the screen closes.
    }
```

## Displaying Your Screen

You can Display your screen in many ways, for example using a [broken-reference](broken-reference/ "mention") implementation, or opening it when a key is pressed using [onekeybind.md](../utils/onekeybind.md "mention"). They can be opened easily using `GuiUtils.displayScreen(new MyScreen())`.
