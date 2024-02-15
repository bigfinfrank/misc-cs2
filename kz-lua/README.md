# Counter-Strike 2 KZ Lua VScript *(forked from https://github.com/DEAFPS/cs2-kz-lua)*

KZ lua vscript with changes for my personal private server

- Works in multiplayer (the original was solo only)
- Includes per-session personal best
- Doesn't count vertical longjumps

## Instructions

### Prerequisite

You'll need vscript enabled, which isn't the case by default and Valve doesn't include an official way to enable this, so we have two methods available:

1. If you already are, are planning to, or don't mind using metamod and metamod plugins, you can use https://github.com/Source2ZE/LuaUnlocker (or if you have CS2Fixes, this functionality is already unlocked).
2. If you don't want to use metamod or don't want to use the plugin, you can directly patch vscript.dll to enable it, see https://github.com/bklol/vscriptPatch

### Installation

Assuming you've already enabled vscript, installation is pretty simple:
1. Find your game installation, this is typically "`C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\`", if you're having trouble, right click Counter-Strike 2 in your steam library, hover over "Manage", and click "Browse local files" you should see folders like "bin", "content", "csgo", "game", and "platform" (note: cs2.exe isn't directly in this folder, it's in `game\bin\win64`, so don't fret)

2. Go into `\game\csgo\` and create the folder "scripts", now go into your newly created scripts folder, and create another folder inside that one called "vscripts", your folder structure should now look something like `C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\game\csgo\scripts\vscripts`.

3. Download and place [`kz.lua`](https://github.com/bigfinfrank/misc-cs2/blob/main/kz-lua/kz.lua) into this folder by copy pasting, clicking the download arrow in the top right of that page, or clicking raw in the top right of that page and using CTRL + S/right click -> "Save Page As".

4. Add `sv_cheats "true"; script_reload_code "kz";`, to the bottom of `/game/csgo/cfg/gamemode_competitive.cfg`, if you don't want sv_cheats enabled, you can append ` sv_cheats "false";`, this will ensure the KZ vscript loads whenever your server/client loads a new map (note: this file might be erased when updating/validating game files, so you might want to consider creating/modifying a file in the same folder named `server_custom.cfg`)

### Usage

#### Tracking & Overlay

The HUD popup overlay and stat tracking (Personal bests as well as chat notifications on longjump) are both done automatically once the script is loaded and a player has connected. You may need to reconnect to get your name to update after a map change, however if you see no special HUD element you likely didn't correctly install the script, or need to change map to get it to apply.

#### Checkpoints

To create a checkpoint you can use the `kz_cp` command in console.
To teleport to a checkpoint, you can use the `kz_tp` command in console.

Both of these can be bound (in this example, to the side buttons on your mouse) like this: `bind "MOUSE4" "kz_cp"; bind "MOUSE5" "kz_tp";`

### Demonstration

This demonstration is by DEAFPS, the creator of the repository this was originally forked from, it doesn't necessarily reflect exactly how the script now behaves as I've made some changes and the video might have been made with an outdated version of the script, but it still shows the general idea pretty clearly.

https://github.com/DEAFPS/cs2-kz-lua/assets/43534349/8f6a27e7-4d70-4db2-bf92-217c88cea156
