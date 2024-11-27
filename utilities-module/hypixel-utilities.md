# Hypixel Utilities

OneConfig's utils module provides a set of Hypixel-specific utility methods for a better development experience.

## Getting server-side info about the client player (rank, prefix, etc)

{% tabs %}
{% tab title="Java" %}
```java
HypixelUtils.PlayerInfo playerInfo = HypixelUtils.getPlayerInfo();
Optional<PlayerRank> playerRank = playerInfo.getRank(); // NORMAL, YOUTUBER, GAME MASTER or ADMIN
Optional<PackageRank> packageRank = playerInfo.getPackageRank(); // NONE, VIP, VIP PLUS, MVP, MVP PLUS
Optional<MonthlyPackageRank> monthlyPackageRank = player.getMonthlyPackageRank(); // NONE, SUPERSTAR
Optional<String> prefix = playerInfo.getPrefix();
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val playerInfo = HypixelUtils.getPlayerInfo()
val playerRank = playerInfo.getRank().getOrNull() // NORMAL, YOUTUBER, GAME MASTER or ADMIN
val packageRank = playerInfo.getPackageRank().getOrNull() // NONE, VIP, VIP PLUS, MVP, MVP PLUS
val monthlyPackageRank = player.getMonthlyPackageRank().getOrNull() // NONE, SUPERSTAR
val prefix = playerInfo.getPrefix().getOrNull()
```
{% endtab %}
{% endtabs %}

All of the custom data types contained within `PlayerInfo` come from the [Hypixel HypixelData ](https://github.com/HypixelDev/HypixelData)library.

## Getting info about the player's current party

{% tabs %}
{% tab title="Java" %}
```java
HypixelUtils.PartyInfo partyInfo = HypixelUtils.getPartyInfo();
boolean isInParty = partyInfo.isInParty();
int partySize = partyInfo.getPartySize(); // Returns 0 if the client player is not in a party
Map<UUID, ClientboundPartyInfoPacket.PartyMember> members = partyInfo.getMembers();
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val partyInfo = HypixelUtils.getPartyInfo()
val isInParty = partyInfo.isInParty()
val partySize = partyInfo.getPartySize() // Returns 0 if the client player is not in a party
val members: Map<UUID, ClientboundPartyInfoPacket.PartyMember> = partyInfo.getMembers()
```
{% endtab %}
{% endtabs %}

All of the custom data types contained within `PartyInfo` come from the [Hypixel ModAPI](https://github.com/HypixelDev/ModAPI) library.

## Getting info about the client player's location on the Hypixel Network

{% tabs %}
{% tab title="undefined" %}
```java
HypixelUtils.Location location = HypixelUtils.getLocation();
Optional<String> lastServerName = location.getLastServerName();
Optional<String> serverName = location.getServerName();
Optional<String> lastLobbyName = location.getLastLobbyName();
Optional<String> lobbyName = location.getLobbyName();
Optional<String> lastMapName = location.getLastMapName();
Optional<String> mapName = location.getMapName();
Optional<String> lastMode = location.getLastMode();
Optional<String> mode = location.getMode();
Optional<ServerType> lastServerType = location.getLastServerType();
Optional<ServerType> serverType = location.getServerType();
boolean wasInLobby = location.wasInLobby();
boolean inLobby = location.inLobby();
boolean wasInGame = location.wasInGame();
boolean inGame = location.inGame();
Optional<GameType> lastGameType = location.getLastGameType();
Optional<GameType> gameType = location.getGameType();
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val location = HypixelUtils.getLocation()
val lastServerName: Optional<String> = location.lastServerName
val serverName: Optional<String> = location.serverName
val lastLobbyName: Optional<String> = location.lastLobbyName
val lobbyName: Optional<String> = location.lobbyName
val lastMapName: Optional<String> = location.lastMapName
val mapName: Optional<String> = location.mapName
val lastMode: Optional<String> = location.lastMode
val mode: Optional<String> = location.mode
val lastServerType: Optional<ServerType> = location.lastServerType
val serverType: Optional<ServerType> = location.serverType
val wasInLobby: Boolean = location.wasInLobby()
val inLobby: Boolean = location.inLobby()
val wasInGame: Boolean = location.wasInGame()
val inGame: Boolean = location.inGame()
val lastGameType: Optional<GameType> = location.lastGameType
val gameType: Optional<GameType> = location.gameType
```
{% endtab %}
{% endtabs %}

All of the custom data types contained within `Location` come from the [Hypixel HypixelData ](https://github.com/HypixelDev/HypixelData)library.
