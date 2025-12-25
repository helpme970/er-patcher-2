# Elden Ring Proton Patcher 2

A tool aimed at enhancing the experience when playing the game by patching the executable so you don't need to mess with .dlls.

> Please note that all these patches may won't work after the release of Elden Ring on the Switch 2, because they might change the engine in a way that breaks this tool. I'll try to update and make it working again if this happens.

## Features
- change fps
- remove 60hz lock in fullscreen
- run without Easy Anti Cheat
- disable rune loss
- remove black bars (useful for ultrawidescreens)
- disable vignette
- disable chromatic abberation
- increase animation distance
- skip intro logos
- always center camera to player
- faster respawn
- fix camera (disables the camera reset when trying to lock-on with no target in range)
- disable camera auto rotate

> All features are Tested with Elden Ring version 1.16.1

> working with and without Shadow of the Erdtree dlc

<details>
<summary><h2>Changes made to er-patcher</h2></summary>

- allow one time/permanent patch
- always center camera to player
- faster respawn
- fix camera (disables the camera reset when trying to lock-on with no target in range)
- disable camera auto rotate
- debug output
- colored output
</details>

## Dependencies
- Python >= 3.8

## Usage

1. Copy the file `er-patcher` to the game directory or specify the path to the game via the `--gamepath` option.
2. In steam, set the game launch options to `python er-patcher ARGS -- %command%` or use permanent patch option. See [Features](#features) for available options.
  - Example for the Steam Deck for one (permanent) patch:

    `python er-patcher --all --rate 30 -p`
    
  - Example:

    `python er-patcher --all --rate 30 --disable-rune-loss -- %command%`

  - Example using the [Seamless Co-op](https://www.nexusmods.com/eldenring/mods/510) mod:

    `python er-patcher --all --executable ersc_launcher.exe -- %command%`

  - Example using the [Seamless Co-op](https://www.nexusmods.com/eldenring/mods/510) mod with permanent patch:

    `python er-patcher --all -p --with-eac`

  - Example using [MangoHud](https://github.com/flightlessmango/MangoHud) and wine fullscreen FSR:

    `python er-patcher --rate 144 -uvca -- env WINE_FULLSCREEN_FSR=1 MANGOHUD=1 MANGOHUD_CONFIG=histogram %command%`

  - Example for enabling HDR using gamescope on Linux (reported to work on Plasma 6.1):

    `ENABLE_GAMESCOPE_WSI=1 DXVK_HDR=1 gamescope -W 3440 -H 1440 -f -r 165 --hdr-enabled -- python er-patcher --all --rate 165 -- %command%`
    
3. Launch the game through steam. `er-patcher` automatically launches a patched version of `eldenring.exe` with EAC disabled.

Note: There might be some distros (e.g. older Ubuntu releases) that launch python 2 instead of 3 when running `python`. In that case you'll need to replace `python` with `python3` in the launch option line. 

## Troubleshooting
If you have issues, verify your game files and make sure that no other patch is applied to Elden Ring.

## Options

| Argument                                | Description                                                                                               |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `-r RATE` or `--rate RATE`              | Set a custom framerate limit (default: 60).                                                               |
| `-x EXE` or `--executable EXE`          | The executable to launch, relative to the games folder.<br>Mutually exclusive with `--with-eac`.          |
| `--with-eac`                            | Run game with EAC (Use it at your own risk).<br>Mutually exclusive with `--executable`.                   |
| `--disable-rune-loss`                   | Disable losing runes upon death.                                                                          |
| `--all`                                 | Enable all options except `--rate`, `--executable`, and<br>gameplay changes like `--disable-rune-loss`.   |
| `-u` or `--ultrawide`                   | Remove black bars.                                                                                        |
| `-v` or `--disable-vignette`            | Remove the vignette overlay.                                                                              |
| `-c` or `--disable-ca`                  | Disable chromatic abberation.                                                                             |
| `-a` or `--increase-animation-distance` | Fix low frame rate animations at screen<br>edges or for distant entities.                                 |
| `-s` or `--skip-intro`                  | Skip intro logos at game start.                                                                           |
| `-f` or `--remove-60hz-fullscreen`      | Remove the 60Hz limit in fullscreen<br>mode (not needed with proton).                                     |
| `-p` or `--permanent`                   | Make the patches permanent.                                                                               |
| `-q` or `--quick-respawn`               | Respawn a few seconds faster.                                                                             |
| `-e` or `--player-camera`               | Always center camera to player.                                                                           |
| `-y` or `--fix-camera`                  | Disables the camera reset when trying to<br>lock-on with no target in range.                              |
| `-b` or `--no-rotate-camera`            | Disable camera auto rotate.                                                                               |
| `-g path/to/game` or `--gamepath path/to/game`| Specify path to game.                                                                               |

## Windows Support

The patcher works just as well on windows. The following launch option line works in case you e.g. installed Python from Microsoft Store:

> `python er-patcher --rate 165 --all -- %command%`

Note: This spawns a python console which will close by itself after the game has finished running. If you find this annoying you can try using `pythonw` instead. In any case `python` needs to be in PATH for windows to find it.

Note 2: Ensure Vertical Sync is turned off for Elden Ring in Nvidia Control Panel / AMD Radeon Software / Intel Graphics Command Center, otherwise the custom framerate limit feature won't work.

## How it works

When the game is launched through steam, the tool creates a patched version of `eldenring.exe` in a temporary subdirectory while leaving the original intact. As long the flag `--with-eac` is not set, the tool modifies the steam launch command to launch the patched executable instead of `start_protected_game.exe`, thefore ensuring that the patched exe is never run with EAC enabled. After the game is closed, the patched executable is removed.

## Credits
- [er-patcher](https://github.com/gurrgur/er-patcher) by gurrgur, they did the most work, I just changed some things in their project
- [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - frame time limit adjustment
  - black bar removal
- [Flawless Widescreen](https://www.flawlesswidescreen.org)
  - vignette and ca removal
  - animation distance increase
- [DarkSouls3RemoveIntroScreens](https://github.com/bladecoding/DarkSouls3RemoveIntroScreens): intro logo skip
- [EldenRingMods](https://github.com/techiew/EldenRingMods) + [EldenRingFpsUnlockAndMore](https://github.com/uberhalit/EldenRingFpsUnlockAndMore)
  - disable rune loss
  - camera fix + no rotate camera
- [Center Camera on Player](https://github.com/ImAxel0/EldenRing-CenterCameraOnPlayer-Mod/)
- [Faster Respawn](https://github.com/ImAxel0/EldenRing-FasterRespawn-Mod/)
- let me know if I forgot your contribution
