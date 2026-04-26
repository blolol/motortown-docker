-----------------------------
[How to Run Dedicated Server]
-----------------------------
1. Rename DedicatedServerConfig_Sample.json to DedicatedServerConfig.json.
2. Edit DedicatedServerConfig.json.
3. For a quick start, review these fields first:
   - <ServerName>
   - <MaxPlayers>
   - <Password> (optional)
4. Review the grouped settings below and adjust as needed.
5. Launch the dedicated server using RunDedicatedServer.bat or through the Steam Library (Steam login required).

-------------------------
[Basic Server Settings]
-------------------------
- <ServerName>: This will be shown on the server list.
- <ServerMessage>: Shown to players after they connect (use \n for a new line).
- <Password>: Optional password required to join the server.
- <MaxPlayers>: Recommended 20 for average systems; maximum 100.

---------------------------
[Gameplay / World Settings]
---------------------------
- <MaxVehiclePerPlayer>: Limits how many vehicles a single player can spawn.
- <Rain>: Set 0 to disable rain. Set 1(Low) ~ 4(Always) to change rain frequency. Set -1 to use user setting in Saved/Config/WindowsServer/GameUserSettings.ini
- <Fire>: Set 0 to disable fire. Set 1(Low) ~ 4(Very High) to change wild fire frequency. Set -1 to use user setting in Saved/Config/WindowsServer/GameUserSettings.ini
- <NPCVehicleDensity>: Sets the density of NPC traffic. Range: 0 (none) to 10 (maximum).
- <NPCPoliceDensity>: Sets the density of NPC police vehicles. Range: 0 (none) to 10 (maximum).

---------------------------
[Housing / Company Settings]
---------------------------
- <bAllowPlayerToJoinWithCompanyVehicles>: Set 'true' to allow joining with company-owned vehicles.
- <bAllowCompanyAIDriver>: Set 'true' to allow company AI driver.
- <bAllowCorporation>: Set 'false' to disable corporation creation (defaults to true).
- <bAllowCorporationAIDriver>: Set 'false' to disable corporation AI drivers (defaults to true).
- <MaxHousingPlotRentalPerPlayer>: Maximum housing plots one player can rent simultaneously.
- <MaxHousingPlotRentalDays>: Duration (in days) a player can rent a housing plot.
- <HousingPlotRentalPriceRatio>: Multiplier that adjusts housing rental pricing.

--------------------------------
[Security / Validation Settings]
--------------------------------
- <bAllowModdedVehicle>: Set 'true' to permit modded vehicles on the server.
- <GameDataValidation> (optional): Controls which GameDataHash mismatches are allowed.
  If omitted, all mismatch types are allowed by default and periodic runtime validation will not start.
  Example:
    "GameDataValidation": {
      "bAllowVehicleAndPartsMismatch": true,
      "bAllowCargoMismatch": true,
      "bAllowItemMismatch": true,
      "bAllowConsoleVariableMismatch": true,
      "bAllowBalanceTableMismatch": true
    }
  Set any field to 'false' to disallow that mismatch type.
  Periodic runtime validation starts only when at least one mismatch type is disallowed.

-------------------------
[Host Web API Settings]
-------------------------
- <bEnableHostWebAPIServer>: Enable the Host Web API (defaults to false).
- <HostWebAPIServerPassword>: Password used by the Host Web API. Do not use your personal password. Use random words.
- <HostWebAPIServerPort>: Port number served by the Host Web API (default 8080).
- <HostWebAPIDisabledCommands>: List any Web API commands that should be disabled (defaults to empty).
- <HostWebAPIOptions>: Endpoint specific options (advanced). Array of { "Endpoint": "<path>", "Params": { <string key>: <string value> } }.

-------------------------
[Admin / Role Settings]
-------------------------
- <Admins>: Add admin entries to this list. To obtain the required UniqueNetId and nickname:
  1. Start the server and connect via the game client.
  2. Grant admin rights to the desired player.
  3. Open %LOCALAPPDATA%\MotorTown\Saved\Config\Windows\GameUserSettings.ini
  4. Search for the 'Admins' section and copy the unique_id/nickname pair.
- <bAllowPoliceVehicleByPlayerRole>: Set 'true' to restrict police vehicles by player role; 'false' allows any player.
- <PoliceRolePlayers>: List players who should receive the police role permissions. Only used when bAllowPoliceVehicleByPlayerRole is true.
- <bAllowAdminToRemoveAdmin>: Set 'true' to allow admins to remove other admins (defaults to false).

-----------------
[Save Files Path]
-----------------
Saved\SaveGames
(You can copy your Client Game Save files into this folder from '%LOCALAPPDATA%\MotorTown\Saved\SaveGames')

---------------------
[Host Web API Server]
---------------------
See 'Host Web API Settings' above for DedicatedServerConfig.json fields.
Refer to WebApiReadme.txt for Host Web API endpoint documentation.
