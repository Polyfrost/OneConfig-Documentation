---
description: Here you will learn how to create options inside OneConfig.
---

# Config Options

## Adding options

### Creation

Options are added with Java annotations. Any field you annotate with an option will be saved to your config file, which you earlier specified in it's constructor. It'll then be displayed to the user within the OneConfig GUI.

```java
@Switch(
    name = "A random switch",
    size = OptionSize.DUAL, // optional, declares whether the element is single column or dual column
    category = "General", // optional
    subcategory = "Switches" // optional
)
public static boolean bob = false; // this is the default value.
```

### Accessing

Retrieving the value of your options is incredibly easy, as seen in the example below!

```java
System.out.println("My thing in a variable called bob: " + MyConfig.bob);
System.out.println("Is this enabled? " + MyConfig.enabled);
```

{% hint style="info" %}
Subcategories and Options are displayed in the order they are put in the config. You can have multiple subcategories with the same name, but this is not recommended unless it genuinely makes sense (e.g. "HUD Options" for two separate types of HUDs).
{% endhint %}

## Disabling Options

Disabled options are still visible to the user, but cannot be interacted with. You can disable them by adding dependencies.

If you wish to do this, go back to your config's constructer, and put in an `addDependency` line, as seen below. The first argument will specify which variable should be edited, given the value of the second argument.&#x20;

```java
@Switch(
    name = "Master Switch",
    size = OptionSize.DUAL
)
public static boolean masterSwitch = false;

@Switch(
    name = "Sub Switch",
    type = OptionType.SWITCH,
)
public static boolean subSwitch = false;

public TestConfig() {
    super(new Mod("My Mod", ModType.UTIL_QOL), "mymod.json");
    addDependency("subSwitch", () -> masterSwitch); // disable subSwitch if masterSwitch is off, making it dependant
}
```

## Other option features

### Sizes

Options come in two sizes in the GUI, `SINGLE` and `DUAL`. These are stored in a simple enum called `OptionSize`. Here is what a single and dual Text Field look like:

![Difference between Single and Dual Variants of a Text Field](<../../.gitbook/assets/image (2).png>)

## Option types

There are lots to choose from, so what are you waiting for?

{% content-ref url="boolean-config-components.md" %}
[boolean-config-components.md](boolean-config-components.md)
{% endcontent-ref %}

{% content-ref url="number-config-components.md" %}
[number-config-components.md](number-config-components.md)
{% endcontent-ref %}

{% content-ref url="multi-config-components.md" %}
[multi-config-components.md](multi-config-components.md)
{% endcontent-ref %}

{% content-ref url="text-configs.md" %}
[text-configs.md](text-configs.md)
{% endcontent-ref %}

{% content-ref url="buttons-colors-and-keybinds.md" %}
[buttons-colors-and-keybinds.md](buttons-colors-and-keybinds.md)
{% endcontent-ref %}

{% content-ref url="decorative-config-components.md" %}
[decorative-config-components.md](decorative-config-components.md)
{% endcontent-ref %}
