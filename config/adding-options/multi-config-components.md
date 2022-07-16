---
description: Learn about components that allow the user to select between multiple options.
---

# Selector Configs

## Dropdown List

A dropdown is a simple list that allows for one option to be selected from a list. They are commonly used for things that have modes. It, as usual, has dual and single-column variants.

It has a String array of options, which you can fill with as many as you like. The variable output is set as the index of that option in the list.

```java
@Dropdown(
    name = "I drop!",        // name of the component
    options = {"An option", "Another option", "Maybe this one?", "Or this!"},
)
public static int value = 1;        // defualt option (here "Another Option")
```

![Dropdown example, open and closed with list](<../../.gitbook/assets/image (9).png>)
