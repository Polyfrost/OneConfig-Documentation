---
description: These components are only used to provide structure and information
---

# Decorative config components

## Header

The header is the most basic decoration, it is just text above or beside config options. \
It takes no extra arguments.\
It has a 1x and 2x varient.

```java
@Option(
    name = "Header",
    type = OptionType.HEADER,
    size = 1, // optional
    category = "General", // optional
    subcategory = "Example" // optional
)
public static boolean ignored;
```

## Info Line

An info line is used to provide info or a warning about something.\
It takes an extra argument that says what icon it should use. Types you can use are: INFO, WARNING, ERROR and SUCCESS\
It has a 1x and 2x varient.

```java
@Option(
    name = "Info Line",
    type = OptionType.INFO,
    infoType = InfoType.INFO,
    size = 1,
    category = "General", // optional
    subcategory = "Example" // optional
)
public static boolean ignored;
```

## Custom Pages

You can have Page buttons on your Config page, using the @Page annotation. You can specify a class that extends Page under this, and when it is clicked it will open that page. To create your own page, check out [#custom-pages](../../gui/pages.md#custom-pages "mention") for more information on them.
