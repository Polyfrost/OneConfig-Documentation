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
    size = OptionSize.DUAL, // optional, declares weather the element is single colum or dual column
    category = "General", // optional, declares wher
    subcategory = "Switches" // optional
)
public static boolean bob = false; // this is the defualt value.
```

Options are displayed in the order they are put in the config.

Subcategories are also displayed in the order they are put in the config. You can have multiple subcategories with the same name.

## Disabling Options

Options can be disabled by adding a dependency to them, to do this, simply go into the constructor of the config and add a line with `addDependency` with the first argument being the variable name and the second argument is the condition that has to be true for the config element to be enabled

```java
@Option(
    name = "Master Switch",
    type = OptionType.SWITCH,
)
public static boolean masterSwitch = false;

@Option(
    name = "Sub Switch",
    type = OptionType.SWITCH,
)
public static boolean subSwitch = false;

public TestConfig() {
    super(new Mod("My Mod", ModType.UTIL_QOL, "creator", "v1.0"), "config.json");
    addDependency("subSwitch", () -> masterSwitch);
}
```

## Option types

{% content-ref url="boolean-config-components.md" %}
[boolean-config-components.md](boolean-config-components.md)
{% endcontent-ref %}

{% content-ref url="number-config-components.md" %}
[number-config-components.md](number-config-components.md)
{% endcontent-ref %}

{% content-ref url="multi-config-components.md" %}
[multi-config-components.md](multi-config-components.md)
{% endcontent-ref %}

{% content-ref url="decorative-config-components.md" %}
[decorative-config-components.md](decorative-config-components.md)
{% endcontent-ref %}
