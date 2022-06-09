---
description: >-
  Here you will learn how to use config components that allow the user to select
  between multiple options
---

# Multi config components

## Dropdown

A dropdown takes an options argument that has all the options and stores the current value as an integer.\
It has a 1x and 2x varient

```java
@Option(
    name = "Dropdown",
    type = OptionType.DROPDOWN,
    options = {"Option 1", "Option 2", "Option 3", "Option 4"},
    size = 1, // optional
    category = "General", // optional
    subcategory = "Example" // optional
)
public static int value = 0;
```

## Arrow Uniselect

An arrow uniselect also takes an options argument that has all of the options and stores the current value as an integer.\
It has a 1x and 2x varient

```java
@Option(
    name = "Dropdown",
    type = OptionType.UNI_SELECTOR,
    options = {"Option 1", "Option 2", "Option 3", "Option 4"},
    size = 1, // optional
    category = "General", // optional
    subcategory = "Example" // optional
)
public static int value = 0;
```
