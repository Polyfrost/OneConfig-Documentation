# IO Utilities

## Clipboard manipulation

OneConfig no longer provides in-house utilities for managing the user's clipboard; however, we do include [Deftu's Copycat library](https://github.com/Deftu/Copycat), which uses native code to bypass any issues brought on by certain operating systems (such as macOS disallowing headless apps from using the AWT clipboard API).

### Obtaining a clipboard instance

```java
Clipboard clipboard = Clipboard.getInstance();
```

The default implementation of `Clipboard` uses the natives provided by Copycat. Calling the `getInstance` method will automatically load the natives should it need to.

### Copying and getting strings

{% tabs %}
{% tab title="Java" %}
```java
String clipboardString = clipboard.getString();
if (clipboardString == null) {
    // If the user does not have anything copied, or the copied content
    // is not a string (if, f.ex, it's an image), then the `getString`
    // method returns null.
    return;
}

String newClipboardString = "Hello, OneConfig!";
clipboard.setString(newClipboardString); // Copies our string to the user's clipboard
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val clipboardString = clipboard.getString()
if (clipboardString == null) {
    // If the user does not have anything copied, or the copied content
    // is not a string (if, f.ex, it's an image), then the `getString`
    // method returns null.
    return
}

val newClipboardString = "Hello, OneConfig!"
clipboard.setString(newClipboardString) // Copies our string to the user's clipboard
```
{% endtab %}
{% endtabs %}

### Copying and getting images

{% tabs %}
{% tab title="Java" %}
```java
ClipboardImage clipboardImage = clipboard.getImage();
if (clipboardString == null) {
    // If the user does not have anything copied, or the copied content
    // is not a string (if, f.ex, it's an image), then the `getString`
    // method returns null.
    return;
}

ClipboardImage newClipboardImage = null; // Obtain your image somehow...
clipboard.setImage(newClipboardImage); // Copies our string to the user's clipboard
```
{% endtab %}

{% tab title="Kotlin" %}
```
String clipboardString = clipboard.getString();
if (clipboardString == null) {
    // If the user does not have anything copied, or the copied content
    // is not a string (if, f.ex, it's an image), then the `getString`
    // method returns null.
    return;
}

String newClipboardString = "Hello, OneConfig!";
clipboard.setString(newClipboardString); // Copies our string to the user's clipboard
```
{% endtab %}
{% endtabs %}

By default, `ClipboardImage` on it's own is simply two `int`s for the `width` x `height`, and an array of bytes for the raw image data. Thus meaning, that should you want to make use of it in any meaningful way, you'll need to convert it to another type for another library OR handle the raw bytes on your own. Thankfully, Copycat provides a means of converting to and from the Java AWT types for you, which you can find below.

### Copying AWT images (BufferedImage)

{% tabs %}
{% tab title="Java" %}
```java
BufferedImage ourImage = ImageIO.read("/path/to/your/image");
// Now, we can't simply copy the above image as it is because we need
// a ClipboardImage, not a BufferedImage.

// So, we'll convert it using this subtype.
ClipboardImage ourClipboardImage = BufferedClipboardImage.toClipboardImage(ourImage);

// Now, we can finally copy it.
Clipboard clipboard = Clipboard.getInstance();
clipboard.setImage(ourClipboardImage);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val ourImage = ImageIO.read("/path/to/your/image")
// Now, we can't simply copy the above image as it is because we need
// a ClipboardImage, not a BufferedImage.

// So, we'll convert it using this subtype.
val ourClipboardImage: ClipboardImage = BufferedClipboardImage.toClipboardImage(ourImage)

// Now, we can finally copy it.
val clipboard = Clipboard.getInstance()
clipboard.setImage(ourClipboardImage)
```
{% endtab %}
{% endtabs %}

This works vice-versa too!

{% tabs %}
{% tab title="Java" %}
```java
Clipboard clipboard = Clipboard.getInstance();
ClipboardImage clipboardImage = clipboard.getImage();

// Now, we just need to convert it to a BufferedImage
BufferedImage image = BufferedClipboardImage.toBufferedImage(clipboardImage);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val clipboard = Clipboard.getInstance()
val clipboardImage = clipboard.getImage()

// Now, we just need to convert it to a BufferedImage
val image = BufferedClipboardImage.toBufferedImage(clipboardImage)
```
{% endtab %}
{% endtabs %}

## File checksums (SHA-256 only)

OneConfig provides a single, ease-to-use method for obtaining the checksum of a file at a given path.

{% tabs %}
{% tab title="Java" %}
```java
Path myFilePath = Paths.get("/path/to/your/file");
String sha256Checksum = IOUtils.getFileChecksum(myFilePath);

// Couldn't obtain the file's checksum
if (sha256Checksum.isEmpty()) {
    return;
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val myFilePath = Paths.get("/path/to/your/file")
val sha256Checksum = IOUtils.getFileChecksum(myFilePath)

// Couldn't obtain the file's checksum
if (sha256Checksum.isEmpty()) {
    return
}
```
{% endtab %}
{% endtabs %}
