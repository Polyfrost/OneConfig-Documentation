# Platform-specific utilities

The `Platform` class in OneConfig's `utils` module is a means to provide several methods which will serve the same function regardless of what Minecraft version or mod loader is currently being used by the player. It serves several general purpose, smaller platform utilities such a localization, mod loader, OpenGL, etc utilities.

## Mod loader platform

### Getting the current Minecraft version

`LoaderPlatform#getMinecraftVersion` (or `Platform.loader().getMinecraftVersion()`) returns a 0-padded representation of the current Minecraft version, f.ex: `11605` or `10809` which represent 1.16.5 and 1.8.9 respectively.

### Getting the current mod loader name

`LoaderPlatform#getLoader` (or `Platform.loader().getLoader()`) returns the current mod loader, represented by the `Loaders` enum, which contains `FORGE` and `FABRIC`.

### Checking if we're in a developer environment

`LoaderPlatform#isDevelopmentEnvironment`(or `Platform.loader().isDevelopmentEnvironment()`) can be used to check if the player is currently inside of a developer environment.

### Checking if a specific mod ID is loaded

`LoaderPlatform#isModLoaded`(or `Platform.loader().isModLoaded(String)`) returns a boolean for if a mod with the given ID is currently loaded.

### Getting all currently loaded mods

`LoaderPlatform#getLoadedMods`(or `Platform.loader().getLoadedMods()`) returns a list of `ActiveMod` instances, all containing information such as a mod's name, ID, version and where it was loaded from (it's source).

## Player platform

### Checking if the player is in multiplayer

`PlayerPlatform#inMultiplayer`(or `Platform.player().inMultiplayer()`) returns a boolean for if the player is currently connected to a multiplayer server or LAN world.

### Checking if the player currently exists (in a world)

`PlayerPlatform#inMultiplayer`(or `Platform.player().inMultiplayer()`) returns a boolean for if the player is currently connected to a multiplayer server or LAN world.

### Getting the player's username



### Getting information about the server the player is connected to



## GL platform



## Screen platform



## I18n platform

