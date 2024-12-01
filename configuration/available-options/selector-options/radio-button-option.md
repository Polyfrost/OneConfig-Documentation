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
    description = "This is my radio", // Recommended, default = ""
    icon = "/my_radio.svg", // Optional, default = ""
    category = "Radio Buttons", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    options = { "HELLO", "WORLD", "ONECONFIG" } // Recommended, default = {}
)
public static int myRadio = 0; // 0 = "HELLO"
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
@RadioButton(
    title = "My Radio",
    description = "This is my radio", // Recommended, default = ""
    icon = "/my_radio.svg", // Optional, default = ""
    category = "Radio Buttons", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    options = ["HELLO", "WORLD", "ONECONFIG"] // Recommended, default = []
)
var myRadio = 0 // 0 = "HELLO"
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
    description = "This is my radio", // Recommended, default = ""
    icon = "/my_radio.svg", // Optional, default = ""
    category = "Radio Buttons", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    // this field cannot be present when using an enum: options = { "HELLO", "WORLD", "ONECONFIG" }
)
public static MyRadioOptions myRadio = MyRadioOptions.HELLO;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
public enum class MyRadioOptions {
    HELLO,
    WORLD,
    ONECONFIG
}

@RadioButton(
    title = "My Radio",
    description = "This is my radio", // Recommended, default = ""
    icon = "/my_radio.svg", // Optional, default = ""
    category = "Radio Buttons", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    // this field cannot be present when using an enum: options = ["HELLO", "WORLD", "ONECONFIG"]
)
var myRadio = MyRadioOptions.HELLO
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Your field can be typed with an integer, or with an enum.

When using an integer, you NEED to provide the `options` property, otherwise it is not supported when using an enum.
{% endhint %}
