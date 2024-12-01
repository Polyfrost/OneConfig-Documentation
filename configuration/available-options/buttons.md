# Buttons

## Example

It's preferable to make your button callback methods to private so that they can't be called elsewhere (unless you want to call them elsewhere yourself manually).

{% tabs %}
{% tab title="Java" %}
```java
@Button(
    title = "My Button",
    description = "This is my button", // Recommended, default = ""
    icon = "/my_button.svg", // Optional, default = ""
    category = "Buttons", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    text = "Say hi!" // Recommended, default = "Click"
)
private void sayHi() {
    System.out.println("Hello, OneConfig!");
}
```
{% endtab %}

{% tab title="Kotlin" %}
<pre class="language-kotlin"><code class="lang-kotlin">@Button(
    title = "My Button",
    description = "This is my button", // Recommended, default = ""
    icon = "/my_button.svg", // Optional, default = ""
    category = "Buttons", // Recommended, default = "General"
    subcategory = "General", // Recommended, default = "General"
    text = "Say hi!" // Recommended, default = "Click"
)
<strong>private fun sayHi() {
</strong>    println("Hello, OneConfig!");
}
</code></pre>
{% endtab %}
{% endtabs %}
