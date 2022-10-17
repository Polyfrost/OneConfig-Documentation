---
description: Learn all about boolean components.
---

# Boolean Configs

## Common booleans

### Switch

The switch is the best way to represent a simple boolean. It's got both a single and dual column variant, and the option you'll use the most.

```java
@Switch(
    name = "Toggle Switch (1x)",
    size = OptionSize.SINGLE // optional
)
public static boolean bob = false;        // default value
```

This code will create a switch like this:

![Toggle Switch example (off and on states)](<../../.gitbook/assets/image (17).png>)

### Checkbox

A checkbox is the best way to represent less important booleans. It's got both single and dual-column variants.

```java
@Checkbox(
    name = "Im a checkbox!",
    size = OptionSize.DUAL // optional
)
public static boolean something = false;        // default value
```

![Checkbox examples (off and on states)](<../../.gitbook/assets/image (4).png>)

### When should you use a switch or checkbox

The switch option is intended for strict ON/OFF options, such as particles. You either see particles, or you don't. In contrast, checkboxes are intended for finer, more detailed control. Maybe you enable potion particles and disable crits.&#x20;

## Dual Option

Out of the three simple config components, dual options are the most unusual. It's got both single and dual-column variants.

{% hint style="info" %}
**Designers note:** These exist for when a simple ON/OFF component wouldn't make sense. Such as a direction, or time of day. Essentially, a boolean that wouldn't make sense with yes/no.
{% endhint %}

```java
@DualOption(
    name = "I can slide!", // name of the element
    left = "I'm Left",     // string to display on the left
    right = "No, right!"   // string to display on the right
)
public static boolean leftyrighty = false;        // default value
```

![](<../../.gitbook/assets/image (7).png>)
