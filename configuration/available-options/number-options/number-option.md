# Number Option

<figure><img src="../../../.gitbook/assets/java_pBxc2rJf8I.png" alt=""><figcaption><p>An example of what the number option looks like in-game.</p></figcaption></figure>

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Number(
    title = "My Number",
    titleKey = "", // Sets the options tile translation key, default = ""
    description = "This is my number", // Sets the options description, default = ""
    descriptionKey = "", // Sets the options description translation key, default = ""
    icon = "/my_number.svg", // Sets the icon used for the option, default = ""
    category = "Numbers", // Sets the options category, default = "General"
    categoryKey = "", // Sets the categories translation key, default = ""
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = "", // Sets the options subcategory translation key, default = ""

    unit = "ms", // Sets the unit, default = ""
    unitKey = "", // Sets the units translation key, default = ""
    min = 0f, // Sets the min value, default = -10
    max = 50f, // Sets the max value, default = 100
    placeholder = "", // Sets the placeholder, default = ""
    placeholderKey = "" // Sets the placeholder translation key, default = "oneconfig.numberinput.placeholder"
)
public static float myNumber = 0f;
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
var myNumber: Float by number(
    name = "My Number",
    def = 0f,
    nameKey = null, // Sets the options tile translation key, default = null
    description = "This is my number", // Sets the options description, default = null
    descriptionKey = null, // Sets the options description translation key, default = null
    icon = "/my_number.svg", // Sets the icon used for the option, default = null
    category = "Numbers", // Sets the options category, default = "General"
    categoryKey = null, // Sets the categories translation key, default = null
    subcategory = "General", // Sets the options subcategory, default = "General"
    subcategoryKey = null, // Sets the options subcategory translation key, default = null

    unit = "ms", // Sets the unit, default = null
    unitKey = null, // Sets the units translation key, default = null
    min = 0f, // Sets the min value, default = -10
    max = 50f, // Sets the max value, default = 100
    placeholder = null, // Sets the placeholder, default = null
    placeholderKey = null // Sets the placeholder translation key, default = "oneconfig.numberinput.placeholder"
)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Your field can be typed with any subtype of `Number`.
{% endhint %}
