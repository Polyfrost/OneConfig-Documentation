---
description: Learn about components that allow the user to select between multiple options.
---

# Selector Configs

## Dropdown List

A dropdown list lets the user select options from a list. If switches are booleans, and sliders are integers, a dropdown is an enum. It's got both single and dual-column variants.

It uses a String Array to list the options and returns its position index within that array. In the example below, the default value is set to 1, which corresponds to the second option.

```java
@Dropdown(
    name = "I drop!",        // name of the component
    options = {"An option", "Another option", "Maybe this one?", "Or this!"},
)
public static int value = 1;        // default option (here "Another Option")
```

![Dropdown example, open and closed with list](<../../.gitbook/assets/image (9).png>)
