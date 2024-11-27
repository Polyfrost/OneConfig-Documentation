# Networking Utilities

There is a small set of basic, yet useful, networking utilities for things such as obtaining a string from a URL, downloading a file, etc.

## Getting a string response from a URL

{% tabs %}
{% tab title="Java" %}
```java
String url = "https://example.com";
String userAgent = "Example/1.0.0";
int timeout = 30_000; // 30 seconds
boolean useCaches = true; // If we request from this same URL multiple times, the response will be cached

String response = NetworkUtils.getString(url, userAgent, timeout, useCaches);
System.out.println("Response from example.com:\n" + response);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val url = "https://example.com"
val userAgent = "Example/1.0.0"
val timeout = 30_000 // 30 seconds
val useCaches = true // If we request from this same URL multiple times, the response will be cached

val response = NetworkUtils.getString(url, userAgent, timeout, useCaches)
println("Response from example.com:\n$response")
```
{% endtab %}
{% endtabs %}

It is recommended to use the name of your mod as the first half of your user agent, and the version as the second half.

Otherwise, you can simply call `getString` using a URL to use the default OneConfig user agent, a timeout of 5000 milliseconds (5 seconds) and no caching.

{% tabs %}
{% tab title="Java" %}
```java
String url = "https://example.com";

String response = NetworkUtils.getString(url);
System.out.println("Response from example.com:\n" + response);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val url = "https://example.com"

val response = NetworkUtils.getString(url)
println("Response from example.com:\n$response")
```
{% endtab %}
{% endtabs %}

## Getting a JSON response from a URL

{% tabs %}
{% tab title="Java" %}
```java
String url = "https://example.com";
JsonElement json = JsonUtils.parseFromUrl(url);

// You can use your JsonElement as you please
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val url = "https://example.com"
val json: JsonElement = JsonUtils.parseFromUrl(url)

// You can use your JsonElement as you please
```
{% endtab %}
{% endtabs %}

## Downloading files

{% tabs %}
{% tab title="Java" %}
```java
String url = "https://example.com";
Path path = Paths.get("/path/to/your/file");
String userAgent = "Example/1.0.0";
int timeout = 30_000; // 30 seconds
boolean useCaches = true; // If we request from this same URL multiple times, the response will be cached

boolean result = NetworkUtils.downloadFile(url, path, userAgent, timeout, useCaches);
System.out.println("File download status: " + result);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val url = "https://example.com"
val path = Paths.get("/path/to/your/file")
val userAgent = "Example/1.0.0"
val timeout = 30_000 // 30 seconds
val useCaches = true // If we request from this same URL multiple times, the response will be cached

val result = NetworkUtils.downloadFile(url, path, userAgent, timeout, useCaches)
println("File download status: $result")
```


{% endtab %}
{% endtabs %}

Again, similarly to `getString`, you can simply call this method with only the URL and path of the downloaded file.

{% tabs %}
{% tab title="Java" %}
```java
String url = "https://example.com";
Path path = Paths.get("/path/to/your/file");

boolean result = NetworkUtils.downloadFile(url, path);
System.out.println("File download status: " + result);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val url = "https://example.com"
val path = Paths.get("/path/to/your/file")

val result = NetworkUtils.downloadFile(url, path)
println("File download status: $result")
```
{% endtab %}
{% endtabs %}

## Opening a link in the user's default browser

```java
String ourUrl = "https://example.com";
NetworkUtils.browseLink(ourUrl);
```
