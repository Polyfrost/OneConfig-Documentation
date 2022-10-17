---
description: Learn about the config components that allow the user to enter text.
---

# Text Configs

## Common text inputs

### Normal Text

The normal text input is a field in which a user can type in a value as a String. Simple as that. It's got both single and dual-column variants.

```java
@Text(
    name = "Write something here!",
    placeholder = "please?",        // optional, text to display when there is nothing written there
    secure = false, multiline = false
)
public static String hi = "";
```

![Example text fields](<../../.gitbook/assets/image (11) (1).png>)

### Text box

Basically the same as a normal text field, but it can have multiple lines. It dynamically changes size based on the amount of text written in it. Since it's meant to hold large bodies of text, it can only be displayed in a single-column variant.

```java
@Text(
    name = "Text box",
    secure = false, multiline = true
)
public static String moretext = "";
```

![Multiline text box examples](<../../.gitbook/assets/image (16).png>)

### When to use text inputs versus boxes

It's pretty obvious. The large text box is used for long Strings or Strings with multiple lines. If you're letting the user change their HUD text, you should use regular text inputs.&#x20;

## Secure Text Input

This has the same functionality as normal text inputs, with the added feature of hiding its content until the user presses the 'show' button. It's got both single and dual-column variants.

{% hint style="warning" %}
**IMPORTANT:** This should ALWAYS be used for passwords, API keys, locations, or any other personal information.
{% endhint %}

```java
@Text(
    name = "Secrets :o :eyes:",
    secure = true, multiline = false
)
public static String shhh = "";
```

![Secure text input example](<../../.gitbook/assets/image (13).png>)
