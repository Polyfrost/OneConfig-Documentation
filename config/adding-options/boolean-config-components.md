---
description: Learn about all boolean components.
---

# Boolean config components

## Switch

The switch is a basic boolean, well switch! It has a single and dual column variant.

```java
@Switch(
    name = "Test Switch",
    size = OptionSize.SINGLE // optional
)
public static boolean enabled = false;
```

This code will create a switch like this (true and false states side by side)

![Switch with true and false state](<../../.gitbook/assets/image (7).png>)

## Checkbox

A basic checkbox. It also has a single and dual column variant:

```java
@Checkbox(
    name = "I'm a checkbox!",
    size = OptionSize.DUAL
)
public static boolean something = false;
```

## Dual Option

The dual option requires you to give 2 options in the option array.\
It has a 1x and 2x varient

```java
@Option(
    name = "Dual Option",
    type = OptionType.DUAL_OPTION,
    options = {"LEFT", "RIGHT"},
    size = 1, // optional
    category = "General", // optional
    subcategory = "Example" // optional
)
public static boolean enabled = false;
```
