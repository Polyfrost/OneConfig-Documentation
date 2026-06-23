# JSON Utilities

## Getting JSON elements from a string

### Unsafe (exceptional) parsing

You can **unsafely (exceptionally)** parse JSON from a string using `JsonUtils.parse(String)`, like so:

```java
JsonElement jsonElement = JsonUtils.parse("{}");
```

If incorrect JSON syntax is passed to this method, GSON (the underlying JSON library) will throw a `JsonSyntaxException`

### Safe parsing

`JsonUtils.parseOrNull` will return the resulting `JsonElement`, or null in case any json errors are encountered.

```java
JsonElement jsonElement1 = JsonUtils.parseOrNull("{}"); // non-null, JsonObject
JsonElement jsonElement2 = JsonUtils.parseOrNull("Hello, OneConfig!"); // null
```

### Safe parsing via callbacks

An additional, method exists for the purpose of running a callback **if** parsing succeeds on the given input.

```java
JsonUtils.parse("{}", (jsonElement) -> {
    System.out.println("I'll print out if the JSON is parsed properly! " + jsonElement);
});
```
