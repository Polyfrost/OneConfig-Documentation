# Switch Option

<figure><img src="../../../.gitbook/assets/java_uYaiwaWS6n.png" alt=""><figcaption><p>An example of what the switch looks like in-game, toggled both on and off.</p></figcaption></figure>

## Example

{% tabs %}
{% tab title="Java" %}
```java
@Switch(
    title = "My Switch",
    description = "This is my switch", // Recommended, default = ""
    icon = "/my_switch.svg", // Optional, default = ""
    category = "Switches", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
public static boolean mySwitch = false;
```
{% endtab %}

{% tab title="Kotlin" %}
<pre class="language-kotlin"><code class="lang-kotlin"><strong>var mySwitch: Boolean by switch(
</strong>    name = "My Switch",
    def = false, // Sets option's default value. Recommended, default = true
    description = "This is my switch", // Recommended, default = ""
    icon = "/my_switch.svg", // Optional, default = ""
    category = "Switches", // Recommended, default = "General"
    subcategory = "General" // Recommended, default = "General"
)
</code></pre>
{% endtab %}
{% endtabs %}
