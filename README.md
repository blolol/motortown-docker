# Motor Town: Behind the Wheel Dedicated Server

[Motor Town: Behind the Wheel](https://store.steampowered.com/app/1369670/Motor_Town_Behind_The_Wheel/) is an open-world driving simulator that combines realistic vehicle physics with a variety of activities like deliveries, racing, and taxi driving. It features single-player and multiplayer modes, offering a relaxing yet engaging driving experience.

This Docker image runs the game's dedicated server on Linux, using [GE-Proton](https://github.com/GloriousEggroll/proton-ge-custom).

<img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1369670/header.jpg?t=1743269133" alt="logo" width="300"/></img>

## Usage

### Steam authentication

Downloading MotorTown's dedicated server requires a Steam account that owns the game. Set the `$STEAM_USERNAME` and `$STEAM_PASSWORD` environment variables to authenticate with Steam:

```sh
docker run -e STEAM_USERNAME=foo -e STEAM_PASSWORD=s3cr3t ghcr.io/blolol/motortown
```

### Volumes

The game server's root will be created at `$SERVER_DIR`. By default, `$SERVER_DIR` is defined in `Dockerfile` as `$DATA_DIR/serverfiles`, where `$DATA_DIR`'s default value is `/serverdata`. So, the default server root path is `/serverdata/serverfiles`. You can mount a Docker volume there to persist the entire Steam installation:

```sh
docker run -v my_motortown_data:/serverdata/serverfiles ghcr.io/blolol/motortown
```

Alternatively, if you only want to persist your server's save files and logs, you can mount a volume at `$SERVER_DIR/MotorTown/Saved` (`/serverdata/serverfiles/MotorTown/Saved` by default).

```sh
docker run -v my_motortown_save:/serverdata/serverfiles/MotorTown/Saved ghcr.io/blolol/motortown
```

### Server configuration

You can configure the game by setting `$GAME_CONFIG_JSON` to a JSON object that will be merged on top of [DedicatedServerConfig_Sample.json](share/DedicatedServerConfig_Sample.json). For example:

```sh
docker run -e GAME_CONFIG_JSON='{"ServerName":"Foo Bar","Password":"s3cr3t"}' ghcr.io/blolol/motortown
```

Before the game server starts, [scripts/start-server.sh](scripts/start-server.sh) merges some sane defaults into the sample config (for example, setting `"Admins":[]`) before merging in the contents of `$GAME_CONFIG_JSON` and writing the resulting file to `$SERVER_DIR/DedicatedServerConfig.json`.

### Game updates

Like other [SteamCMD](https://developer.valvesoftware.com/wiki/SteamCMD)-based game server images, this one attempts to update to the latest version of the game on each container startup. So if the game updates, simply restart the container to upgrade it. You can optionally set `$VALIDATE` to `true` to validate the server files:

```sh
docker run -e VALIDATE=true ghcr.io/blolol/motortown
```

## Credits

This repo combines the work of [sazquatch17/motortowndedi](https://github.com/sazquatch17/motortowndedi) and [dominicrico/motortown](https://github.com/dominicrico/motortown). Thanks!
