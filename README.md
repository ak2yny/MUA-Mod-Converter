# MUA Mod Converter

Mod converter to convert mods from MarvelMods for MUA 2006 PC to other platforms.
Based on [Raven-Formats scripts](https://github.com/EthanReed517/Marvel-Mods-Batch-Scripts/blob/main/Raven-Formats%20Scripts/(RF)AIO.bat), but outdated.
Currently supports conversion to Steam, PS3, PS2 and PSP.

For those who like to add their insight to MUA console modding, PS4 and X1 sound formats or other workflows.


## Instructions

(example for PS3)
  1. Extract a mod into any folder.
  2. Make any modifications for the mod in this folder, such as installing boosters, fixing skins, etc.
  3. Extract these tools into the same folder (complete contents).
     If necessary, install the requirements.
     Note: there is no build that you can extract, currently.
  5. Optional: Put packages/generated/maps/package/menus/characters_heads.fb in the same folder.
               (Consoles only, if the mannequin should be added to the package)
  6. Run ModConverter_PCtoPS3.bat
  7. A new folder with the same name plus a "- for PS3" suffix is created next to the mod folder.
     Use the contents of this folder for adding the mod to the PS3:
     - packages go into the assets
     - add the herostat to the PS3 herostat.engb (with OHS or your preferred method) and add that to assets > data
     - sounds go separate

To change which platform it should convert to, go to line 24 and change `set ForPltfrm=PS3`. E.g. `set ForPltfrm=Steam`. Supported platforms are in the remarks on line 23.


## Requirements

  - [Raven-Formats (by nikita488)](https://github.com/nikita488/raven-formats) or Python 3.8+
  - Alchemy 5
  - (Windows with Powershell and .Net feature enabled)
  - FB tools (by Norrin Radd) for consoles
  - MFAudio (by Muzzle Flash) for Playstation platforms
  - FSbank tools (by Firelight Technologies 2016) for Steam (only requires fsbankcl.exe and its libraries)
  - Optional: xmlb-compile.exe (by NBA2KStuff)


## Known issues

  - Packages are converted using .xmlb extension, but mods usually include .engb files. Combat packages are fixed automatically, but non-combat packages aren't because they should only include certain files. The only .xml binary file included in the non-combat package should be the talents file, which is set-up in the cfgBuilder_info.cfg as .engb, so that shouldn't be a problem. It will be a problem if the non-combat package includes special .xml binary files.
  - Skins aren't converted because they can have normal texture maps, which require DXT5. Skins have to be manually converted, if necessary. (Step 2)
  - 6th generation console (and XML2 PC) conversions don't convert any IGB files at all, because the platforms don't support Alchemy 5 processes. Replace the IGB files with platform compatible assets. (Step 2)
  - Doesn't work in locations that require elevated (admin) permission (no matter if the user has these permissions or not).


## Credits

  - ak2yny for the batch script
  - BaconWizard17 for FB batch tool code and testing
  - Jayglass for discovering PS3 requirements and testing
  - Lars for exploring sound mods on the Steam version
  - damarioculbreath for testing
