# Dropdown Option

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption><p>An example of what the dropdown looks like in-game.</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/java_0C55HfZVwg.png" alt=""><figcaption><p>An example of what the dropdown looks like in-game when it is expanded.</p></figcaption></figure>

## Example

## TODO: Redo Kotlin example with Kotlin DSL for enumerables and dropdowns

### Using an integer index

{% tabs %}
{% tab title="Java" %}
```java
@Dropdown(
    title = "My Dropdown",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my dropdown", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_dropdown.svg", // Sets the icon used for the option, default = ""
    category = "Dropdowns", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    options = { "HELLO", "WORLD", "ONECONFIG" }, // Recommended, default = {}
    optionsKey = { } // Allows for translating entries, default = {}
)
public static int myDropdown = 0; // 0 = "HELLO"
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@Dropdown(
    title = "My Dropdown",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my dropdown", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_dropdown.svg", // Sets the icon used for the option, default = ""
    category = "Dropdowns", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    options = [ "HELLO", "WORLD", "ONECONFIG" ], // Recommended, default = {}
    optionsKey = [ ] // Allows for translating entries, default = {}
)
var myDropdown = 0 // 0 = "HELLO"
```
{% endtab %}
{% endtabs %}

### Using a custom enum class

{% tabs %}
{% tab title="Java" %}
```java
public enum MyDropdownOptions {
    HELLO,
    WORLD,
    ONECONFIG;
}

@Dropdown(
    title = "My Dropdown",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my dropdown", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_dropdown.svg", // Sets the icon used for the option, default = ""
    category = "Dropdowns", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    // this field cannot be present when using an enum: options = { "HELLO", "WORLD", "ONECONFIG" }, // Recommended, default = {}
    optionsKey = { } // Allows for translating entries, default = {}
)
public static MyDropdownOptions myDropdown = MyDropdownOptions.HELLO;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
enum class MyDropdownOptions {
    HELLO,
    WORLD,
    ONECONFIG
}

@Dropdown(
    title = "My Dropdown",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my dropdown", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_dropdown.svg", // Sets the icon used for the option, default = ""
    category = "Dropdowns", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    // this field cannot be present when using an enum: options = [ "HELLO", "WORLD", "ONECONFIG" ], // Recommended, default = {}
    optionsKey = [ ] // Allows for translating entries, default = {}
)
var myDropdown = MyDropdownOptions.HELLO
```
{% endtab %}
{% endtabs %}
