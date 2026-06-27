# Radio Button Option

<figure><img src="../../../.gitbook/assets/java_qLmE0Cnfa7.png" alt=""><figcaption><p>An example of what the radio button looks like in-game.</p></figcaption></figure>

## Example

## TODO: Redo Kotlin example with Kotlin DSL for enumerables and radiobuttons

### Using an integer index

{% tabs %}
{% tab title="Java" %}
```java
@RadioButton(
    title = "My Radio",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my radio", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_radio.svg", // Sets the icon used for the option, default = ""
    category = "Radio Buttons", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    options = { "HELLO", "WORLD", "ONECONFIG" }, // Recommended, default = {}
    optionsKey = { } // Allows for translating entries, default = {}
)
public static int myRadio = 0; // 0 = "HELLO"
```
{% endtab %}

{% tab title="Kotlin" %}

TODO: update to new kotlin api, requires implementation first.

```kotlin
var myRadio: String by radiobutton(
    name = "My Radio",
    defaultOption = "HELLO",
    options = arrayOf("HELLO", "WORLD", "ONECONFIG"),
    nameKey = null, // Sets the options name translation key, default = null
    description = "This is my radio", // Sets the options description, default = null
    descriptionKey = null, // Sets the options description translation key, default = null
    icon = "/my_radio.svg", // Sets the icon used for the option, default = null
    category = "Radio Buttons", // Sets the options category, default = "General"
    categoryKey = null, // Sets the categories translation key, default = null
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = null, // Sets the options subcategory translation key, default = null
    optionKeys = arrayOf(""), // Sets the options translation keys, order same as options, default = arrayOf()
    stringTransformer = { it.lowercase() }, // Sets how to get the name for the option, default = { it.toString() }
)
```
{% endtab %}
{% endtabs %}

### Using a custom enum class

{% tabs %}
{% tab title="Java" %}
```java
public enum MyRadioOptions {
    HELLO,
    WORLD,
    ONECONFIG;
}

@RadioButton(
    title = "My Radio",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my radio", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_radio.svg", // Sets the icon used for the option, default = ""
    category = "Radio Buttons", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""
    // this field cannot be present when using an enum: options = { "HELLO", "WORLD", "ONECONFIG" }, // Recommended, default = {}
    optionsKey = { } // Allows for translating entries, default = {}
)
public static MyRadioOptions myRadio = MyRadioOptions.HELLO;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
enum class MyRadioOptions(val displayName: String) {
    HELLO("hi"),
    WORLD("world"),
    ONECONFIG("OneConfig!"),
}

var myRadio by radiobutton(
    name = "My Radio",
    defaultOption = MyRadioOptions.HELLO,
    options = MyRadioOptions.entries.toTypedArray(),
    nameKey = null, // Sets the options name translation key, default = null
    description = "This is my radio", // Sets the options description, default = null
    descriptionKey = null, // Sets the options description translation key, default = null
    icon = "/my_radio.svg", // Sets the icon used for the option, default = null
    category = "Radio Buttons", // Sets the options category, default = "General"
    categoryKey = null, // Sets the categories translation key, default = null
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = null, // Sets the options subcategory translation key, default = null
    optionKeys = arrayOf(""), // Sets the options translation keys, order same as options, default = arrayOf()
    stringTransformer = MyRadioOptions::displayName, // Sets how to get the name for the option, default = { it.toString() }
)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Your field can be typed with an integer, or with an enum.

When using an integer, you NEED to provide the `options` property, otherwise it is not supported when using an enum.
{% endhint %}
