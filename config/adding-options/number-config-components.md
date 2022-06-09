# Number config components

## Slider

The slider can be an integer or a float and has 2 additional options you have to set, min and max.\
It only has a 2x varient

```java
@Option(
    name = "Slider",
    type = OptionType.SLIDER,
    min = 3f, max = 127f,
    category = "General", // optional
    subcategory = "Example" // optional
)
public static float value = 10f;
```

## Stepped Slider

A stepped slider is the same as a normal slider, but it also has a step value.

```java
@Option(
    name = "Stepped Slider",
    type = OptionType.SLIDER,
    min = 0f, max = 30f,
    step = 2,
    category = "General", // optional
    subcategory = "Example" // optional
)
public static float value = 10f;
```
