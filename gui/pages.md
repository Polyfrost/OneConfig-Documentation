---
description: Learn more about OneConfig's pages
---

# Pages

## What are Pages?

Pages are the name given to the displays inside the OneConfig UI, and they are 1056x728 (1024x696 usable) rectangle of the GUI. All the content of OneConfig is displayed inside this area. They are fully scrollable, and you can even make your own pages if you want!&#x20;

![OneConfig Page (highlighted in red)](<../.gitbook/assets/image (8).png>)

## Custom Pages

Custom pages can be created easily by just extending the Page class, like this:

```java
public class MyPage extends Page {
    public MyPage() {
        super("My Page"); // set the name of the page
    }
    
    public void draw(long vg, int x, int y) {
        // draw script for the page
    }
    
    // SCROLLING
    // if you want it to be scrollable, you can use the following methods:
    public int drawStatic(long vg, int x, int y) {
        // draw elements that are not going to be scrollable
        return 12; // return the height of the elements that are drawn in this method
    }
    
    public int getMaxScrollHeight() {
        return 1240; // return the total length of the page (how far can be scrolled)
    }

```

You can use this in combination with a [#custom-pages](../config/adding-options/decorative-config-components.md#custom-pages "mention") decorative config component to open the page, so the user can access it with the click of a button!
