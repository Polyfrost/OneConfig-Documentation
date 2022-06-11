---
description: Rendering text using OneConfig
---

# Font Rendering

## Drawing Text

If you would like to display some text on the screen, you can use the various drawText methods of the `RenderManager`. A list of these can be found on the Dokka docs. These methods work exactly the same as other draw methods to keep it simple:

```java
RenderManager.setupAndDraw((vg) -> {
    // draw Hi! at x=10 y=50 in white (-1), at 12px size in Inter Regular
    RenderManager.drawText(vg, "Hi!", 10, 50, -1, 12f, Fonts.REGULAR);
    
    // draw a string formatted like a URL (blue with underline) at x=10 y=50
    // which can be clicked and hovered
    RenderManager.drawUrl(vg, "https://www.youtube.com/watch?v=dQw4w9WgXcQ", 10, 50, 12f, Fonts.REGULAR);
    
    // draw some wrapped text at x=10 y=50 in white (-1), at 12px in Inter Regular
    // which wraps onto the next line if the line is more than 100px long
    RenderManager.drawWrappedText(vg, "Never gonna give you up; never gonna let you down", 10, 50, 100, -1, 12f, Fonts.REGULAR);
}
```

You can even use your own font by creating a custom `Font` object:

```java
// create the font object
public static final Font inter = new Font("inter", "/path/to/font/file.ttf");

public void draw(long vg, int x, int y) {
    // draw Hi! in your font you chose
    RenderManager.drawText(vg, "Hi!", 10, 50, -1, 12f, inter);
}
```
