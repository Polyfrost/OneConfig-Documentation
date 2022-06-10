---
description: Learn about the config components that allow the user to enter text.
---

# Text Configs

## Normal Text

A normal text input field, which the user can type in. There isn't really that much more to it!\
It has dual and single column variants.

```java
@Text(
    name = "Write something here!",
    placeholder = "please?",        // optional, text to display when there is nothing written there
    secure = false, multiline = false
)
public static String hi = "";
```

![Example text fields](<../../.gitbook/assets/image (11).png>)

## Multiline Text Input

Basically the same as a normal text field, but it can have multiple lines. It dynamically changes size based on the amount of text written in it.\
It only has a dual column variant.

```java
@Text(
    name = "Text box",
    secure = false, multiline = true
)
public static String moretext = "";
```

![Multiline text box examples](<../../.gitbook/assets/image (16).png>)

## Secure Text Input

The same as a normal text input field, but will show text as stars until the show button is pressed. You can use it for passwords, API keys and other secrets. \
It has single and dual column variants.

These are not shared when the profile is shared (coming soon-ish)

```java
@Text(
    name = "Secrets :o :eyes:",
    secure = true, multiline = false
)
public static String shhh = "";
```

![Secure text input example](<../../.gitbook/assets/image (13).png>)
