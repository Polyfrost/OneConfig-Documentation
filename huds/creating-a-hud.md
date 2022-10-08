---
description: Learn about the HUD system OneConfig has to offer
---

# HUD Basics

### What are HUDs?

HUDs are small pieces of information rendered on the player's screen which can display all kinds of things, from images to coordinates. These use an extensive positioning and scaling system built into OneConfig, and this helps us achieve our goal of being able to edit everything for every mod in one place.

OneConfig HUDs are extremely easy to use, with little code needed to create a HUD, and positioning, scaling and everything else handled behind the scenes by OneConfig!

Huds are essentially an extension to the Config system, with a few extra methods, and follow the same syntax for adding additional configuration options to your hud, using annotated fields. (see [creating-a-config.md](../config/creating-a-config.md "mention"))



### Creating a HUD

To create a HUD, all you have to do is extend the class you would like. OneConfig by default has SingleTextHud and TextHud for premade, text only HUDs. These are purely convenience classes which offer an easier way for the most common type of HUD.

This guide will focus on creating a simple HUD that extends SingleTextHud, but if you want to create a more advanced HUD, you should use the BasicHud class instead.

```java
public class MyHud extends SingleTextHud {
    // you can use this to add additional saved config values to your HUD class,
    // just like a normal config.
    int times = 0;
    @Switch(
            name = "Custom Option"
    )
    public boolean yes;
    

    public MyHud() {
        // this is the name of the HUD as shown in the config,
        // and if it is enabled by default
        super("Time", true);
    }

    // this method is called every ingame tick. It is used to update the text shown
    // on the hud. If you need to update this every render tick, you can override
    // getTextFrequent() instead (not recommended)
    @Override
    public String getText(boolean example) {
        // example determines whether or not the HUD is in 'example' mode, which
        // means the user has the Edit HUD screen open. This should ideally be static
        // so that it does not change while the user is moving around their huds,
        // and should give an accurate representation of how the hud will look ingame. 
        if(example) return "I'm in Example mode";
        times++;
        return String.valueOf(times);
    }
}
```

For more information on how to create more advanced HUDs, and to see the wealth of methods that the BasicHud has to offer, make sure to checkout its javadocs, and the [test.huds package of OneConfig.](https://github.com/Polyfrost/OneConfig/tree/master/versions/src/main/java/cc/polyfrost/oneconfig/test/huds)

### Using a HUD

Now you have created a HUD class, you can use it by adding it as a field to your main config class, with the @HUD annotation, just like this:

```java
@HUD(
        name = "Test HUD",
        category = "HUD"
)
public MyHud hud = new MyHud();
```





Simple right? I hope this has given you a basic understanding of how HUDs work in OneConfig, and why they are useful and how powerful they are to use!
