---
description: Learn all about boolean components.
---

# Boolean Configs

## Switch

The switch is a basic boolean, well switch! It has a single and dual column variant. The switch is probably the most common component we offer.

```java
@Switch(
    name = "Toggle Switch (1x)",
    size = OptionSize.SINGLE // optional
)
public static boolean bob = false;        // default value
```

This code will create a switch like this:

![Toggle Switch example (off and on states)](<../../.gitbook/assets/image (17).png>)

## Checkbox

A basic checkbox for checking of things. It also has a single and dual column variant:

```java
@Checkbox(
    name = "Im a checkbox!",
    size = OptionSize.DUAL // optional
)
public static boolean something = false;        // default value
```

![Checkbox examples (off and on states)](<../../.gitbook/assets/image (4).png>)

## Dual Option

The dual option is a simple config component that allows for more clarity, for example in a boolean that determines whether to display something on the Left, or on the Right. It has nice animations.

As always, it has a single and dual column variant.

```java
@DualOption(
    name = "I can slide!", // name of the element
    left = "I'm Left",     // string to display on the left
    right = "No, right!"   // string to display on the right
)
public static boolean leftyrighty = false;        // default value
```

![](<../../.gitbook/assets/image (7).png>)
