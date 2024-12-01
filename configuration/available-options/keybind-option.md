# Keybind Option

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Keybind(
    title = "My Keybind",
    description = "This is my keybind", // Recommended, default = ""
    icon = "/my_keybind.svg", // Optional, default = ""
    category = "Keybinds", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
public static KeyBinder.Bind myKeybind = KeybindHelper.builder().keys(UKeyboard.KEY_NONE).does(() -> {
    System.out.println("Hello, OneConfig!");
}).build();

public MyConfig() {
    registerKeybind(myKeybind);
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val myKeybind: KeyBinder.Bind by keybind(
    name = "My Keybind",
    def = KeybindHelper.builder().keys(UKeyboard.KEY_NONE).does {
        println("Hello, OneConfig!")
    }.build(), // Sets option's default value. Recommended, default = null
    description = "This is my keybind", // Recommended, default = ""
    icon = "/my_keybind.svg", // Optional, default = ""
    category = "Keybinds", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)

init {
    registerKeybind(myKeybind)
}
```
{% endtab %}
{% endtabs %}
