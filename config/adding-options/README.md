---
description: Here you will learn how to create options inside OneConfig.
---

# Adding options

Options are added with an @annotation, a really handy Java feature. Any field annotated with one of the various option types is saved to the file you specified in your constructor earlier, and will be displayed inside the OneConfig GUI as an option for the user to change.

You can access your config's values statically like this:

```java
System.out.println("My thing in a variable called bob: " + MyConfig.bob);
System.out.println("Is this enabled? " + MyConfig.enabled);
```

Here is an example of how an option should look:

```java
@Switch(
    name = "A random switch",
    size = OptionSize.DUAL, // optional, declares weather the element is single column or dual column
    category = "General", // optional
    subcategory = "Switches" // optional
)
public static boolean bob = false; // this is the defualt value.
```

{% hint style="info" %}
Subcategories and Options are displayed in the order they are put in the config. You can have multiple subcategories with the same name, but this is not recommended unless it genuinely makes sense (e.g. "HUD Options" for two separate types of HUDs).
{% endhint %}

## Disabling Options

Options can be disabled by adding a dependency to them. When they are disabled, they cannot be interacted with by the user and are shown grayed out for clarity.&#x20;

If you want to do this, simply go into the constructor of your config and add an`addDependency` clause, with the **String argument being the variable name of the one you want to be dependant**, and the **second argument is the condition that has to be true** for the config element to be enabled.&#x20;

If you like, you can set this to be an if statement, or another config component, as in the example:

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

## Option Sizes

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
