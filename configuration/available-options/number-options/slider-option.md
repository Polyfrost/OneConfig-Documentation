# Slider Option

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Slider(
    title = "My Slider",
    description = "This is my slider", // Recommended, default = ""
    icon = "/my_slider.svg", // Optional, default = ""
    category = "Sliders", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    min = 0f, // Recommended, default = 0f
    max = 100f, // Recommended, default = 100f
    step = 1f // Optional, default = 10f
)
public static float mySlider = 0f;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
var mySlider: Float by slider(
    name = "My Slider",
    def = 0f, // Sets option's default value. Recommended, default = 0f
    description = "This is my switch", // Recommended, default = ""
    icon = "/my_switch.svg", // Optional, default = ""
    category = "Switches", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    min = 0f, // Recommended, default = 0f
    max = 100f, // Recommended, default = 100f
    step = 1f, // Optional, default = 10f
)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Your field can be typed with any subtype of `Number`.
{% endhint %}
