# `cs2_video.txt` Community Documentation and Modification Instructions

First of all, `cs2_video.txt` is the file where Valve stores Counter-Strike 2's graphics settings. However it doesn't just store them how they're presented in the graphics settings menu in-game, instead storing them as console variables (AKA convars/cvars). Normally this would mean we can just change them via the console, however this isn't possible without modifying the game files as (almost) all of these settings are protected with the "defensive"/"developmentonly" flags. This means that *(normally)* in order to change or even check the current value of them*, you need to modify a file that will mark your game as VAC insecure until you've reverted the change, meaning you can't join VAC secured servers, but we can tweak these values in the file they're stored in with a bit of tinkering and they'll remain until we change graphics settings in-game.

*we'll touch back on this fact a bit later.

## Modification

If we play around with this file, it gives us the ability to fine tune our graphics settings to a much greater extend than Valve allows us to do normally. This gives us three main approaches that serve unique benefits, and I recommend you to mix and match these key ideas as you see fit:

1. You can increase fidelity beyond what would ordinarilly be possible, for example by increasing shadow distance and resolution, at the cost of performance. If you have a significant excess of FPS and don't mind the drop, or are recording a video and want the highest quality, this can serve extremely useful.

2. On the opposite end of the spectrum, you can decrease fidelity significantlly lower than the game would normally allow, letting you get much better performance than you can by simply setting all of your graphics settings to their lowest available options in-game. In some extreme cases this may even make the difference between the game being unplayable and reasonably acceptable.

3. Sort of in-between, if you're mostly happy with where you're at in terms of performance, or simply don't want to sacrified the competitive advantages you get by upping your shadow settings for example, this will let you selectively increase 'parts' of a graphics setting without all of them, for example only showing play shadows and not geometry shadows. while still maintaining a high shadow render distance and high shadow quality.A

### Important tips  ***(YOU SERIOUSLY WILL WANT TO READ THESE)***

> [!IMPORTANT]
> Seriously, read the first few sentences of each section, I've intentionally included all the information you'll need to determine if you want to skip the tip.

#### Testing Changes

Since we can't normally modify these options at run-time, it gets pretty annoying to make one change, start the game, load into a map, check the effect it had, close the game, repeat. We can avoid this by *temporarily* modifying `csgo_core\gameinfo.gi` to allow us to adjust Defensive convars at runtime.

1. Find your game installation, this is typically "`C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\`", if you're having trouble, right click Counter-Strike 2 in your steam library, hover over "Manage", and click "Browse local files" you should see folders like "bin", "content", "csgo", "game", and "platform" (note: cs2.exe isn't directly in this folder, it's in `game\bin\win64`, so don't fret)

2. Go into `\game\csgo_core\` and create a copy of gameinfo.gi, this will let us easily revert the change without verifying game files, which would also revert changes made to other modified files if you have any. Your folder structure should look something like this `C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\game\csgo_core\`, you should see other files like gameinfo_branchspecific.gi, and several VPK files prefixed with pak and shaders_, **make sure you're in csgo_core, not just "core" or "csgo" and not csgo_addons/csgo_imported/csgo_lv**.

3. Open gameinfo.gi (**not** gameinfo_branchspecific.gi) and at around line 140, you should find a line that reads as follows `		"DefensiveConCommands"	"1"`, change that "1" to a "0" to 'lower their defenses'. If you're having trouble finding it and are sure you're in csgo_core\gameinfo.gi, not a different gameinfo.gi file, then:
- If you're familiar with Valve's KeyValues format, this is nested within "GameInfo" -> MaterialSystem2 -> Engine2.
- If you're note familiar with this format, and you think colored syntax highlighting will help you find it, ~~see the Syntax Highlighting section below~~. (Coming Soon, tldr use https://code.visualstudio.com/ with https://marketplace.visualstudio.com/items?itemName=ChaosInitiative.source-tools even though we're not coding here, code editors like this one are basically just extremely versatile and well-built text editors that are perfectly suited for a problem like this)

4. Save the file, open the game, and open up console. Run `help "cl_log_tick";`, it should say there's no cvar or command named cl_log_tick, that's expected, if it gives you help info, then filter by defensive here and pick a different convar to test with [here](https://cs2.poggu.me/dumped-data/convar-list). Now without anything before or after, just run `cl_log_tick;` (note: auto-complete suggestions won't include defensive convars, even when enabled), if it simply puts "> cl_log_tick;" in console with no response, you messed up one of the previous steps, however if it responds with the current value, ex. "[Console] cl_log_tick = false", you're good to go.

5. Continue on, this means you can test cs2_video.txt's defensive convars in-game without restarting every single time.
