# UEMultiplayerSessionsPlugin
Unreal Engine multiplayer sessions plugin for Steam.

Built for UE 4.27 and 5 - C++ project - not tested with a Blueprint only project.
This plugin is a work in progress, I decided to make it public so you can have fun, experiment and learn from my mistakes ;)

Created following Stephen Ulibarri's Unreal Engine 5 C++ Multiplayer Shooter course on Udemy (https://www.udemy.com/share/1069OE3@dbcCDCrMuKt6uEQTvFDNQYJ3oSLZ8c5kT8N0s_GDiA3gjTzIt6Z-FPZcNsuPoxN9gQ==/)

Good official UE info here: https://docs.unrealengine.com/5.0/en-US/online-subsystem-steam-interface/

Enable the Steam stuff first, then we can add the MultiplayerSessions plugin.

Open UE game.
Enable the OnlineSubsystemSteam plugin. Edit -> Plugins -> search for Online Subsystem Steam
Restart will likely be required.

Goto the "Config" folder in the project's directory (same as the Plugin folder)
Edit the following:

**Note: SteamDevAppId=480 is the generic test app id for Steam, this is only used for testing.**

---------

File: DefaultEngine.ini

Add:
```
[/Script/Engine.GameEngine]
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="OnlineSubsystemSteam.SteamNetDriver",DriverClassNameFallback="OnlineSubsystemUtils.IpNetDriver")

[OnlineSubsystem]
DefaultPlatformService=Steam

[OnlineSubsystemSteam]
bEnabled=true
SteamDevAppId=480
bInitServerOnClient = true

[/Script/OnlineSubsystemSteam.SteamNetDriver]
NetConnectionClassName="OnlineSubsystemSteam.SteamNetConnection"

```
----------------

OPTIONAL - just to override the UE default max players.

File: DefaultGame.ini

Add:
```
[/Script/Engine.GameSession]
MaxPlayers=100
```
-----------------

You can now add the MultiplayerSessions plugin.

UE/project should be closed.
Copy whole MultiplayerSessions folder to the Plugins folder in the project directory (ie. via windows explorer, main project directory - same as *.uproject file) - if no "Plugins" folder exists, create a new one.

Close the project, right-click on the .uproject file and select "Generate Visual Studio Project Files"
Deleting the "Intermediate" and "Binaries" folders in both the main directory and Plugins/MultiplayerSessions may be requred before generating visual studio files.

**In Editor:**

The plugin UI needs to be added to a level.

Create a new level for your multiplayer menu (and a Level BP if you want a custom one), open the level Blueprint, drag off of the Event BeginPlay node, select Create Widget (adding a new widget construstor node), in the Class field select WBP_Menu from the dropdown, drag off of this node and search for Menu Setup.

In Menu Setup change the Lobby Path to the path of your lobby level, use the same format as the default field text - /Game/ is used in place of /Content/ and do not include the .umap extension.

Number Of Public Connections: can be set to anything you like - this is the max number of players that can join.

Type Of Match: can be anything you like but only matches of the same type will be discoverable.

That should be it... Have FUN!!
