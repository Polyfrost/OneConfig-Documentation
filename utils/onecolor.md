---
description: Learn more about OneColor, OneConfig's way of processing colors
---

# OneColor

## Why?

OneColor exists for many reasons.

Firstly, there are limitations when converting RGB to HSB and vice versa. We wanted to have HSB color selectors because they are much more usable than a few RGB sliders. Rendering uses ARGB though, so we have to convert! This means multiple conversions for RGB to HSB every tick, and there can be miscalculations with this.

Secondly, we wanted to have a more lightweight alternative to `java.awt.Color`. While it's not bad for performance, it contains a lot of code that isn't strictly necessary, so we built a more lightweight alternative. There are many similarities to `Color` in terms of methods and language for parity, but they are different under the hood.

Lastly, we wanted to support chroma **natively.** So, we have a data bit, which controls the speed of the chroma, along with favorites, and the `getRGB()` methods will return these chroma colors instantly.

So, in a nutshell, we made OneColor for performance and accuracy.

## OneColor's structure

OneColor stores color as a `short[]` array, creating an `int rgba` every time the color is changed (upon instantiation). They are used with the @Color Config element, are used widely throughout OneConfig's codebase and are fully integrated with `java.awt.Color` and [colorutils.md](available-utilities/colorutils.md "mention").

```java
short hue = 240;          // hue of the color (0-360)
short saturation = 50;    // saturation of the color (0-100)
short brightness = 25;    // brightness of the color (0-100)
short alpha = 255;        // alpha of the color (0-255)

int argb = -38279103;    // the color stored as ARGB merged integer (used for rendering)

// how ARGB is made (hexadecimal):
// 0xFF000000 alpha (0-FF)
// 0x00FF0000 red (0-FF)
// 0x0000FF00 blue (0-FF)
// 0x000000FF green (0-FF)
// when merged with bitshifts, it will return the color as an integer like above.
```

## Creating a OneColor

Creating a OneColor is very easy! Here are some of the methods you can use:

```java
public OneColor color = new OneColor(int red, int green, int blue, int alpha);
public OneColor color = new OneColor(int red, int green, int blue);
public OneColor color = new OneColor(float hue, float saturation, float brightness, float alpha);
public OneColor color = new OneColor(float hue, float saturation, float brightness);
public OneColor color = new OneColor(java.awt.Color);
public OneColor color = new OneColor(int argb);
```

## Hex

OneColor also has full support for hex strings. You can create a OneColor from a parsed hex, or get the hex of a OneColor easily.

The hex parser has **auto-completion features**, and supports a variety of hexes even if they are malformed:

- If the hex is less than 6 characters, 0s are appended.
- If the hex is 3 characters long, it is understood as a 3-digit RGB hex and is repeated appropriately.
  - E.g. CF2 -> CCFF22.
- If the hex is 1 character long, it is repeated across the R, G and B fields.&#x20;
  - E.g. C -> CCCCCC.
- The alpha will be fetched from the hex color if it is 8 characters long (RRGGBBAA).
