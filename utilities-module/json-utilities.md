# JSON Utilities

## Getting JSON elements from a string

### Unsafe (exceptional) parsing

You can **unsafely (exceptionally)** parse JSON from a string using `JsonUtils#parse(String)`, like so:

```java
JsonElement jsonElement = JsonUtils.parse("{}");
```

If incorrect JSON syntax is passed to this method, GSON will throw a `JsonSyntaxException`

### Safe parsing

`JsonUtils#parseOrNull` will automatically catch any exceptions thrown by GSON's parser and return the resulting `JsonElement` or null if a parsing error was thrown. It can be used like so:

```java
JsonElement jsonElement1 = JsonUtils.parseOrNull("{}"); // non-null, JsonObject
JsonElement jsonElement2 = JsonUtils.parseOrNull("Hello, OneConfig!"); // null
```

### Safe parsing via callbacks

An additional, third method is present for the purpose of running a callback **if** parsing succeeds on the string given.

```java
JsonUtils.parse("{}", (jsonElement) -> {
    System.out.println("I'll print out if the JSON is parsed properly! " + jsonElement);
});
```
