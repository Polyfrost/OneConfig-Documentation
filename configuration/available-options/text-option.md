# Text Option

<figure><img src="../../.gitbook/assets/java_WIFWo2mAw5.png" alt=""><figcaption><p>An example of what the text option looks like in-game.</p></figcaption></figure>

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Text(
    title = "My Text",
    description = "This is my text", // Recommended, default = ""
    icon = "/my_text.svg", // Optional, default = ""
    category = "Text", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    placeholder = "Name..." // Optional, default = "polyui.textinput.placeholder"
)
public static String myText = "";
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
var myText: String by text(
    title = "My Text",
    def = "", // Sets option's default value. Recommended, default = ""
    description = "This is my text", // Recommended, default = ""
    icon = "/my_text.svg", // Optional, default = ""
    category = "Text", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    placeholder = "Name..." // Optional, default = "polyui.textinput.placeholder"
)
```
{% endtab %}
{% endtabs %}
