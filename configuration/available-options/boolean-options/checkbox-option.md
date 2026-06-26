# Checkbox Option

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Checkbox(
    title = "My Checkbox",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my checkbox", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_checkbox.svg", // Sets the icon used for the option, default = ""
    category = "Checkboxes", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "" // Sets the options subcategory translation key, default = ""
)
public static boolean myCheckbox = false;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
var myCheckbox: Boolean by checkbox(
    name = "My Checkbox",
    def = true, // Default value, required
    titleKey = null, // Sets the options tile translation key, default = null
    description = "This is my checkbox", // Sets the options description, default = null
    descriptionKey = null, // Sets the options description translation key, default = null
    icon = "/my_checkbox.svg", // Sets the icon used for the option, default = null
    category = "Checkboxes", // Sets the options category, default = "General"
    categoryKey = null, // Sets the categories translation key, default = null
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = null // Sets the options subcategory translation key, default = null
)
```
{% endtab %}
{% endtabs %}
