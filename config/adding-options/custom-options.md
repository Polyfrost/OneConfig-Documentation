---
description: Learn how to create custom options with OneConfig.
---

# Custom options

### Creating an option

First you have to create an option, to do this create a class that extends the BasicOption class and implement all methods.

```java
public class MyOption extends BasicOption {

    public MyOption(Field field, Object parent, String name, String category, String subcategory, int size) {
        super(field, parent, name, category, subcategory, size);
    }

    @Override
    public void draw(long vg, int x, int y) {
        // draw everything here
    }

    @Override
    public int getHeight() {
        return 32; // return the height of the option so other options can be placed accordingly
    }
}
```

### Basic usage

The easiest way to use a custom option is to annotate the field `CustomOption` annotation and specify an id.

```java
@CustomOption(id = "myOption")
public static boolean yes = true;
```

Then too add your option to the config system you have to overwrite the `getCustomOption` method in the config, add the option to the page using `ConfigUtils` and then return the option. Here is an example implementation:

```java
@Overwrite
protected BasicOption getCustomOption(Field field, CustomOption annotation, OptionPage page, Mod mod, boolean migrate) {
    BasicOption option = null;
    switch (annotation.id()) {
        case "myOption":
            option = new MyOption();
            ConfigUtils.getSubCategory(page, "category", "subcategory").options.add(option);
            break;
    }
    return option;
}
```

### Advanced usage

Using it in the way described previously is not a good option in the following situations:

* You have to use the option multiple times in different categories and subcategories
* The option has options that aren't always the same

A better alternative in these situations is to create an annotation that is annotated with the  `CustomOption` annotation.

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
@CustomOption(id = "myOption")
public @interface MyOptionAnnotation {
    String category();
    String subcategory();
    int exampleVariable();
}
```

Then to implement this you have to modify your `getCustomOption` a bit.

```java
@Overwrite
protected BasicOption getCustomOption(Field field, CustomOption annotation, OptionPage page, Mod mod, boolean migrate) {
    BasicOption option = null;
    switch (annotation.id()) {
        case "myOption":
            MyOptionAnnotation myOption =  ConfigUtils.findAnnotation(field, MyOptionAnnotation.class);
            option = new MyOption(myOption.exampleVariable());
            ConfigUtils.getSubCategory(page, myOption.category(), myOption.subcategory()).options.add(option);
            break;
    }
    return option;
}
```
