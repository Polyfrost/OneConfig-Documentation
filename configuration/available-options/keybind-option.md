# Keybind Option

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Keybind(
    title = "My Keybind",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my info block", // Recommended, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "", // Optional, default = "". Please refer to Notifications.Type to see default types
    category = "Decorations", // Recommended, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Recommended, default = "General"
    subcategoryKey = "" // Sets the options subcategory translation key, default = ""
)
public static KeyBinder.Bind myKeybind = KeybindHelper.builder().key(UKeyboard.KEY_NONE).action(() -> {
    System.out.println("Hello, OneConfig!");
}).register();
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val myKeybind: KeyBinder.Bind by keybind(
    name = "My Keybind",
    def = KeybindHelper.builder().key(UKeyboard.KEY_NONE).action {
        println("Hello, OneConfig!")
    }.register(), // Sets option's default value. Recommended, default = null
    nameKey = null, // Sets the options tile translation key, default = null
    description = null, // Sets the options description, default = null
    descriptionKey = null, // Sets the options description translation key, default = null
    icon = null, // Sets the icon used for the option, default = null
    category = "General", // Sets the options category, default = "General"
    categoryKey = null, // Sets the categories translation key, default = null
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = null, // Sets the options subcategory translation key, default = null
)

init {
    registerKeybind(myKeybind)
}
```
{% endtab %}
{% endtabs %}
