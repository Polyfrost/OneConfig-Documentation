# Platform-specific utilities

The `Platform` class in OneConfig's `utils` module is a means to provide several methods which will serve the same function regardless of what Minecraft version or mod loader is currently being used by the player. It contains a wide variety of methods that are both general purpose, but also smaller utilities.

## Mod loader platform

The loader platform (obtained through `Platform.loader()`) can be used to access mod loader information regardless of what loader your project uses.

### Getting the mod loader + version

Calling `LoaderPlatform#getLoaderString` gives you a string that's formatted like the following `<version>-<loader>` so if the player is using fabric and is on 26.1 it would be `26.1-fabric` 


## Screen platform

The screen platform (obtained through `Platform.screen()`) contains methods to get display related information, set screens, get the current screen, and more.

## I18n platform

The I18n platform (obtained through `Platform.i18n()`) contains methods for translating text using the minecraft translation system, and for turning chat components into Strings.

