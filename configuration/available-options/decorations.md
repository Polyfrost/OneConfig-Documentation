# Decorations

## Info

{% tabs %}
{% tab title="Java" %}
```java
@Info(
    title = "My Info Block",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my info block", // Recommended, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_info.svg", // Optional, default = "". Please refer to Notifications.Type to see default types
    category = "Decorations", // Recommended, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Recommended, default = "General"
    subcategoryKey = "" // Sets the options subcategory translation key, default = ""
)
private void info1() {} // Can be anything, methods are just easiest to write.
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Info(
    title = "My Info Block",
    titleKey = null, // Sets the options tile translation key, default = ""
    description = "This is my info block", // Recommended, default = ""
    descriptionKey = null, // Sets the options description translation key, default = ""
    icon = "/my_info.svg", // Optional, default = "". Please refer to Notifications.Type to see default types
    category = "Decorations", // Recommended, default = "General"
    categoryKey = null, // Sets the categories translation key, default = ""
    subcategory = "General", // Recommended, default = "General"
    subcategoryKey = null // Sets the options subcategory translation key, default = ""
)
fun info1() {}
```
{% endtab %}
{% endtabs %}
