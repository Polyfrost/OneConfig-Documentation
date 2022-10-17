---
description: >-
  Learn about the decorations that you can add to your configs to make them
  prettier!
---

# Decorative Components

## Separation

### Header

The header lets you write a title for the following options, helping you separate large mods. You might define all of your colors in a single section, titled "Colors". Or locate all of your HUD options together.

```java
@Header(
    text = "Some information that you need to look at!"
)
public static boolean ignored; // Useless. Java limitations with @annotation.
```

![An info example with some config components beneath it](<../../.gitbook/assets/image (3).png>)

### Custom Pages

Config pages can be used with the @Page annotation. You can specify an additional class that extends Page, which will be opened when clicked. Read more about [#custom-pages](../../gui/pages.md#custom-pages "mention") for more information.

The enum `PageLocation` describes the location of that page, which can either be `TOP` or `BOTTOM`.

```java
@Page(
    name = "I'm a page button!",
    location = PageLocation.TOP,
    // optional description that is also displayed on the page button
    description = "Press me to open a new page!"
)
public static MyPage pageToOpen = new MyPage();
```

![Page button example beneath some other config components](<../../.gitbook/assets/image (10) (1).png>)

## Inline documentation

### Info Line

Information lines can provide the user with extra context about something. Maybe warning the user of a potential issue or common problem you could encounter. It's got both single and dual-column variants. Read the designer's note to understand when this should be used.&#x20;

```java
@Info(
    text = "An error occurred :(",
    type = InfoType.ERROR // Types are: INFO, WARNING, ERROR, SUCCESS
)
public static boolean ignored; // Useless. Java limitations with @annotation.

@Info(
    text = "Just trying to say something here",
    type = InfoType.INFO
)
public static boolean ignored2; // Useless. Java limitations with @annotation.
```

![example info fields](<../../.gitbook/assets/image (18).png>)

### Descriptions

TBD. [nextdaydelivery](https://app.gitbook.com/u/1x0TONidc5SHDNY3bD4rdAznn0P2 "mention")

### When to use an info line over a description

Descriptions aren't always shown to the user, only when they hover over the text of an option. This means that if you're simply adding extra info about what something does, use that. Info lines should be for more crucial information, something you actually want them to read.&#x20;
