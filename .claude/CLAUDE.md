# motortown-docker

This repository builds a Docker image that runs a dedicated server for the game Motor Town: Behind the Wheel (https://store.steampowered.com/app/1369670/Motor_Town_Behind_The_Wheel/). It uses a community fork of the Proton Linux compatibility layer to run the Windows game server executable in a Linux Docker container.

## Game server directory layout

In `Dockerfile`, the `DATA_DIR` env var is used as the home directory for the OS user account that is created to run the server software. The `SERVER_DIR` env var is appended to it to create the Motor Town game server installation root. On successful installation, the following directory structure is created in the Docker container:

```
$DATA_DIR/$SERVER_DIR/
├── DedicatedServerConfig_Sample.json (sample game server config file)
├── Engine/
│   ├── (Unreal Engine files; not important to us)
├── MotorTown/
│   ├── Binaries/
│   │   └── (game server executables and libraries)
│   ├── Content/
│   │   └── (Steam distribution content; not important to us)
│   └── Saved/
│       ├── Config/
│       │   ├── CrashReportClient/
│       │   │   └── (crash report files; not important to us)
│       │   └── WindowsServer/
│       │       └── GameUserSettings.ini (game client settings; no impact on server)
│       ├── Logs/
│       │   ├── (no files seem to be written here; purpose unknown)
│       ├── SaveGames/
│       │   ├── Characters/
│       │   │   ├── 0.sav (example player save file)
│       │   │   ├── 0.sav.Backup0 (example player save backup file)
│       │   │   ├── 0.sav.Backup1 (example player save backup file)
│       │   │   └── 0.sav.Backup2 (example player save backup file)
│       │   └── Worlds/
│       │       └── 0
│       │           ├── Island.world (example world save file)
│       │           ├── Island.world.Backup0 (example world save backup file)
│       │           ├── Island.world.Backup1 (example world save backup file)
│       │           └── Island.world.Backup2 (example world save backup file)
│       └── ServerLog/
│           └── 2026.04.26-16.39.39.log (example server log file)
├── ReadMe.txt (dedicated server readme; copied into this repo's `share` directory)
├── RunDedicatedServer.bat (dedicated server start batch script for use in Windows)
├── WebApiReadme.txt (dedicated server HTTP API readme; copied into this repo's `share` directory)
├── _CommonRedist
│   ├── DirectX
│   │   └── Jun2010
│   │       ├── (DirectX files; not important to us)
```

According to `share/dedicated-server-readme.txt`, the server tries to read `$DATA_DIR/$SERVER_DIR/DedicatedServerConfig.json` to configure itself on startup.
