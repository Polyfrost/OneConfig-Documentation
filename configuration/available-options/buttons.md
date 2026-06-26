# Buttons

## Example

It's preferable to make your button callback methods to private so that they can't be called elsewhere (unless you want to call them elsewhere yourself manually).

{% tabs %}
{% tab title="Java" %}
```java
@Button(
    title = "My Button",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my button", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_button.svg", // Sets the icon used for the option, default = ""
    category = "Buttons", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    text = "Say hi!" // Recommended, default = "Click"
)
private void sayHi() {
    System.out.println("Hello, OneConfig!");
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Button(
    title = "My Button",
    titleKey = "", // Sets the options tile translation key, default = ""
    text = "Say hi!", // Recommended, default = "Click"
    description = "This is my button", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_button.svg", // Sets the icon used for the option, default = ""
    category = "Buttons", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
)
fun sayHi() {
    println("Hello, OneConfig!")
}
```
{% endtab %}
{% endtabs %}
