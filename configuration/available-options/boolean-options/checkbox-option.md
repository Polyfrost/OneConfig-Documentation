# Checkbox Option

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Checkbox(
    title = "My Checkbox",
    description = "This is my checkbox", // Recommended, default = ""
    icon = "/my_checkbox.svg", // Optional, default = ""
    category = "Checkboxes", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
public static boolean myCheckbox = false;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
var myCheckbox: Boolean by checkbox(
    name = "My Checkbox",
    def = false, // Sets option's default value. Recommended, default = true
    description = "This is my switch", // Recommended, default = ""
    icon = "/my_switch.svg", // Optional, default = ""
    category = "Switches", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
```
{% endtab %}
{% endtabs %}
