---
description: OneConfig's rendering system, NanoVG and how to use it
---

# NanoVGHelper

OneConfig introduces NanoVG and LWJGL3 as its rendering method, even on older versions of the game. OneConfig has a feature-rich API wrapper for this called `NanoVGHelper`, which allows developers to draw things on the display, from rectangles to circles and images.

NanoVG allows for beautiful, sharp UIs at fast speeds due to its lightweight design and antialiasing methods.

## Getting Started

To draw things using NanoVG, use the `setupAndDraw` method.

```java
NanoVGHelper.INSTANCE.setupAndDraw((vg) -> {
    NanoVGHelper.INSTANCE.drawRoundedRect(vg, 10, 50, 100, 100, -1, 12f);    // draw a white rounded rectangle with corner radius 12 at x=10, y=50 with a width and height of 100
    // do some more drawing
}
```

If Kotlin is being used, the alternative `nanoVG` method can be used. This automatically passes the NanoVG context that is required in Java.

```kotlin
nanoVG {
    drawRoundedRect(10, 50, 100, 100, -1, 12f)
}
```

Make sure to check out the Dokka Javadocs for more information on available methods in NanoVGHelper and RenderManagerDSL.

// todo add hyperlink for javadocs - MoonTidez

## When do I draw?

A great time to draw things on the screen is using the draw() method of [oneuiscreen.md](../../utils/oneuiscreen.md "mention") in your own GUI screen, or you can use [hudrenderevent.md](../../events/available-events/hudrenderevent.md "mention") to draw things on the screen even when the player isn't in a GUI.

## Colors

OneConfig, like many other Java classes such as `java.awt.Color`, use "merged" integers as colors, in ARGB format. See [onecolor.md](../../utils/onecolor.md "mention") to find out more about how to use these colors and what they are.

## Images

OneConfig's NanoVGHelper also has methods to allow you to draw images - even straight from the internet!

These images use accurate scaling methods and antialiasing so you can draw them at virtually any size. Also, if you want, you can use OneConfig's internal enums SVGs and Images to draw icons and things you already see inside the OneConfig GUI:

```java
NanoVGHelper.INSTANCE.drawText(vg, "There is are images below this, and THE DAILY MAIL????", 10, 40, -1, 10, Fonts.REGULAR); // by the way, we go over font rendering in another page
NanoVGHelper.INSTANCE.drawSvg(vg, SVGs.ONECONFIG, 10, 50, 100, 200);
NanoVGHelper.INSTANCE.drawImage(vg, "https://i.dailymail.co.uk/1s/2021/07/29/20/46061771-0-image-a-349_1627585586527.jpg", 10, 50, 100, 200);
```

Please note that this can only render .jpg, .png and .svg files.

## Info Icons

OneConfig also has a handy way to draw info icons to alert the user to various things.

There are 4 types, INFO, WARNING, ERROR, and SUCCESS. You can draw them just like any other thing using NanoVGHelper.

`NanoVGHelper.INSTANCE.drawInfo(vg, InfoType.WARNING, 10, 50, 50f);`

This will draw a warning info icon at x=10 and y=50 with a size of 50px. Simple!
