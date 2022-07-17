---
description: >-
  Learn about the decorations that you can add to your configs to make them
  prettier!
---

# Decorative Components

## Header

The header is the most basic decoration we offer. It can be used to describe a config,  or just as a bit of something to break up your config page if you like.

```java
@Header(
    text = "Some information that you need to look at!"
)
public static boolean ignored;
```

{% hint style="info" %}
You might have noticed it has a very odd variable beneath it, but it is useless. It is never updated. It is there due to limitations of Java which requires an Object for an `@annotation.`
{% endhint %}

![An info example with some config components beneath it](<../../.gitbook/assets/image (3).png>)

## Info Line

An Info line can be used to provide the user with some information on something, for example what a config does, warn of danger, or if something needs updating.

Types you can use are: INFO, WARNING, ERROR and SUCCESS\
It can be displayed in dual or single column.

```java
@Info(
    text = "An error occurred :(",
    type = InfoType.ERROR
)
public static boolean ignored;

@Info(
    text = "Just trying to say something here",
    type = InfoType.INFO
)
public static boolean ignored2;
```

{% hint style="info" %}
You might have noticed it has a variable beneath it, but it is useless. It is never updated. It is there due to limitations of Java which requires an Object for an `@annotation.`
{% endhint %}

![example info fields](<../../.gitbook/assets/image (18).png>)

## Custom Pages

You can have Page buttons on your Config page, using the @Page annotation. You can specify a class that extends Page under this, and when it is clicked it will open that page. To create your own page, check out [#custom-pages](../../gui/pages.md#custom-pages "mention") for more information on them.

`PageLocation` is an enum that describes the location of the page in the list of the config components, and can either be TOP or BOTTOM.

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
