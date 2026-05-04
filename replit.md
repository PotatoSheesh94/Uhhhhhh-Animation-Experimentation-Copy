# Uhhhhhh - Universal Hierarchical 6 Reanimator

A Roblox Lua scripting project featuring a reanimation/animation script with UI, dances, movesets, hat dropping, modding support, and P2P social features.

## Project Overview

This is **not a web application**. It is a Roblox exploit/script project written in Lua, designed to be loaded into Roblox via a loadstring. It has no web server, frontend, or backend.

## Project Structure

- `source/reanim.lua` - Main Roblox Lua script (~9600+ lines). The core reanimation script loaded into Roblox.
- `source/reanim_bak.lua` - Backup of the main script.
- `content/` - Animation files (`.anim`), audio files (`.mp3`), and Lua variant files for dances/movesets.
- `community/` - Community-contributed content and dance files.
- `uiassets/` - UI audio and graphic assets used by the script.
- `goodies/convertion.lua` - Utility Lua script for conversions.
- `tools/` - Python and Lua utility tools:
  - `allinone.py` - All-in-one processing script (AI-assisted).
  - `getassetids.py` - Tool to extract Roblox asset IDs.
  - `rbxm2anim.py` - Converts `.rbxm` (Roblox model) files to `.anim` format.
  - `lua2rbxmx.lua` - Converts Lua animation data to `.rbxmx` format.
  - `verify.lua` - Verifies animation buffer data.
- `images/` - Screenshots and GIF showcases.

## Languages & Runtimes

- **Lua 5.2** - Main scripting language (Roblox uses a Luau dialect, but tools use Lua 5.2)
- **Python 3.12** - Used for conversion/utility tools

## How to Use

### Running the script in Roblox
Use one of these loadstrings in a Roblox exploit executor:

```lua
-- Cached (via GitHub raw):
loadstring(game:HttpGet("https://raw.githubusercontent.com/STEVE-916-create/Uhhhhhh/main/source/reanim.lua"))()

-- Non-cached (via GitHub API):
local a,b,c,g="/STEVE-916-create/Uhhhhhh/","/source/reanim.lua",".github","https://"local d=request({Url=`{g}api{c}.com/repos{a}contents{b}`,Headers={Accept=`application/vnd{c}.VERSION.raw`}})if d.StatusCode~=200 then d.Body=game:HttpGet(`{g}raw{c}usercontent.com{a}main{b}`)end local e,f=loadstring(d.Body)if not e then warn(f)else e()end
```

### Using Python tools
```bash
python3 tools/rbxm2anim.py   # Convert Roblox model to anim
python3 tools/getassetids.py # Extract asset IDs
python3 tools/allinone.py    # All-in-one processing
```

## Dependencies

- No external package dependencies
- Lua 5.2 (available at `/nix/store/.../bin/lua`)
- Python 3.12 standard library (zipfile, struct, base64, re, math, xml)

## P2P Social Features (added to `source/reanim.lua`)

Three new features were added at the end of the main script (before the credits section):

### 1. Uhhhhhh Players List
- A new **"Uhhhhhh Players ▶"** button appears on the main menu, opening a live list of other players in the server who are also running the script.
- Detection is **dual-method**: chat heartbeat (invisible U+2800 Braille-blank prefix, visually empty to other players) sent every 45 seconds, and periodic character-attribute scanning (`_UH6` attribute on Humanoid/HumanoidRootPart).
- A UI notification pops up whenever a new Uhhhhhh user is detected.
- Players are auto-removed from the list when they leave the game or stop sending heartbeats.

### 2. Sync Dance
- A **"Broadcast Current Dance to Uhhhhhh Users"** button appears at the top of the Dances page.
- Pressing it sends an invisible chat message containing the current dance's internal name.
- Other Uhhhhhh users with **"Auto-Accept Sync Dance"** toggled on will automatically switch to that dance and see a notification showing who initiated the sync.
- Toggle: **Auto-Accept Sync Dance** (on/off switch in main menu).

### 3. No Collision with Uhhhhhh Users
- Toggle: **"No Collision with Uhhhhhh Users"** (on/off switch in main menu, saved to save file).
- When enabled, a background loop runs every 0.2 s and sets `CanCollide = false` (via both direct assignment and `sethiddenproperty`) on all BaseParts belonging to detected Uhhhhhh users' characters.
- This prevents physical collisions from disturbing their reanimation poses or animations.

## Notes

- The script is designed to run inside Roblox's Luau environment, which provides Roblox-specific globals (`game`, `workspace`, `cloneref`, etc.) not available in standard Lua.
- The Python tools are standalone utilities for processing animation files offline.
- The P2P heartbeat chat messages use U+2800 (Braille blank), which renders as an empty line in Roblox chat and is invisible to other players.
