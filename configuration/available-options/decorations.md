# Decorations

## Info

{% tabs %}
{% tab title="Java" %}
```java
@Info(
    title = "My Info Block",
    description = "This is my info block", // Recommended, default = ""
    icon = "/my_info.svg", // Optional, default = "". Please refer to Notifications.Type to see default types
    category = "Decorations", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
private void info1() {} // Can be anything, methods are just easiest to write.
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Info(
    title = "My Info Block",
    description = "This is my info block", // Recommended, default = ""
    icon = "/my_info.svg", // Optional, default = "". Please refer to Notifications.Type to see default types
    category = "Decorations", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
fun info1() {}
```
{% endtab %}
{% endtabs %}
