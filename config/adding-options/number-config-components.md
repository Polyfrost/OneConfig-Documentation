---
description: Learn all about the number config components in OneConfig
---

# Number Configs

## Slider

The slider is a basic draggable element, often used for numbers that control something like the width of an element. It can be an integer or a float, you can choose!

Sliders also have a little number input box at the side to allow for the user to input a number manually if they like.

```java
@Slider(
    name = "You slide me right round baby right round",
    min = 0f, max = 100f        // min and max values for the slider
    // if you like, you can use step to set a step value for the slider,
    // giving it little steps that the slider snaps to.
    step = 10f
)
public static float slideyboi = 50f; // default value
```

![Slider examples (stepped and normal)](<../../.gitbook/assets/image (8).png>)

{% hint style="info" %}
So its not really cramped, a slider can only be displayed in a dual column style.
{% endhint %}

## Number Input

The number input is an adapted text field that only accepts valid number values. It similarly can be a float or integer. It can be displayed in either a dual or single column mode.

It also has cute little arrows next to it which can be clicked to increase or decrease the number by the `step` value (default 1)

```java
@Number(
    name = "I am a number",    // name of the component
    min = 0, max = 37,        // min and max values (anything above/below is set to the max/min
    step = 5        // each time the arrow is clicked it will increase/decrease by this amount
)
public static int num = 20; // defualt value
```

// todo add image
