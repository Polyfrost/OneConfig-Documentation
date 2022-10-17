---
description: >-
  Learn about the button, color and keybind elements that can be used in a
  config.
---

# Buttons, Colors and Keybinds

## Buttons

### Common button

The button is a simple interaction that can trigger code when pressed. It's got both single and dual-column variants.

You can create your method to run when the button is pressed using the Runnable interface:

```java
@Button(
    name = "I'm a button",    // name beside the button
    text = "Click me!"        // text on the button itself
)
Runnable runnable = () -> {    // using a lambda to create the runnable interface.
    System.out.println("I was clicked!");
    FMLCommonHandler.instance().exitJava(69, false);
}
```

![Buttons with single and dual variant examples](<../../.gitbook/assets/image (5).png>)

### Keybinds

OneConfig also offers keybinds that replace Minecraft's own keybind system. Basically, it's handled and stored by OneConfig, not the game. It's got both single and dual-column variants.

{% hint style="success" %}
This config component uses OneKeyBind to store the keybinds.
{% endhint %}

```java
@KeyBind(
    name = "I'm a keybind!"
)
// using OneKeyBind to set the default key combo to Shift+S
public static OneKeyBind keyBind = new OneKeyBind(UKeyboard.KEY_LSHIFT, UKeyboard.KEY_S);
```

To register an action when a keybind is activated, add the following to your constructor:

```java
public Config() {
    registerKeyBind(keyBind, () -> System.out.println("Look mom, a keybind!"));
}
```

![Keybind field examples, including recording state](<../../.gitbook/assets/image (19).png>)

## Colors

The color option lets the user change any default color to their own, using a built-in color picker.

{% hint style="success" %}
This config component uses [onecolor.md](../../utils/onecolor.md "mention") to store the colors.
{% endhint %}

```java
@Color(
    name = "Background Color"
)
OneColor testColor = new OneColor(26, 35, 143);        // default color
```

![Color examples, single and dual column](<../../.gitbook/assets/image (12) (1).png>)

![Color selector GUI examples](<../../.gitbook/assets/image (15).png>)
