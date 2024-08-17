# MUA Mod Converter

Mod converter to convert mods from MarvelMods for MUA 2006 PC to other platforms.
Based on [Raven-Formats scripts](https://github.com/EthanReed517/Marvel-Mods-Batch-Scripts/blob/main/Raven-Formats%20Scripts/(RF)AIO.bat), but outdated.
Currently supports conversion to Steam, PS3, PS2, PSP, GameCube and Wii.

For those who like to add their insight to MUA console modding, PS4 and X1 sound formats or other workflows.


## Requirements

  - [Raven-Formats (by nikita488)](https://github.com/nikita488/raven-formats) or Python 3.9+
  - Alchemy 5 (for IGB asset evaluation and conversion)
  - (Windows with Powershell and .Net feature enabled)
  - [FB tools](https://github.com/EthanReed517/Marvel-Mods-Batch-Scripts/tree/main/FB%20Package%20Tools/FB%20Tools) (by Norrin Radd) for consoles
  - MFAudio (by Muzzle Flash) for Playstation platforms
  - DSPADPCM and dsptool.dll from the GameCube SDK (by Nintendo) for GC and Wii
  - FSbank tools (by Firelight Technologies 2016) for Steam (only requires fsbankcl.exe and its libraries)
  - xmlb-compile.exe (by NBA2KStuff) (required for console package converion)


## Instructions

(example for PS3)
  1. Extract a mod into any empty folder.
     - For **boosters**, but only if the mod's already in the game and only for **console** versions: Instead get the .fb packages from the required mod/character from the assets and put them into any empty folder.
     - For **boosters**, but only if the mod's already in the game and only for **PC** versions: Instead extract the booster into any empty folder.
  2. Make any modifications for the mod in this folder, such as installing boosters, fixing skins, etc. *
  3. Extract these tools into the same folder (complete contents).
     If necessary, install the requirements.
     Note: there is no build that you can extract, currently.
  5. Optional: Put packages/generated/maps/package/menus/characters_heads.fb in the same folder.
               (Consoles only, if the mannequin should be added to the package)
  6. Run ModConverter_PCtoPS3.bat
  7. A new folder with the same name plus a " - for PS3" suffix is created next to the mod folder.
     Use the contents of this folder for adding the mod to the PS3:
     - packages go into the assets (IMPORTANT: All .pkgb files found in the mod are cloned. Some of them might be useless. Adding useless packages might even harm the game.)
     - add the herostat to the PS3 herostat.engb (with OHS or your preferred method) and add that to assets > data
     - sounds go separate (boosters or mods without sounds don't need these)

To change which platform it should convert to, go to line 24 and change `set ForPltfrm=PS3`. E.g. `set ForPltfrm=Steam`. Supported platforms are in the remarks on line 23.

#### * Example Modifications at Step 2

Install Boosters:
  - Extract the booster into the same folder (containing either the required mod, or the required character's .fb package files).
    - The folder structure must match exactly (actors of the booster goes into actors of the already extracted mod, etc.).
    - If the folder doesn't contain the required mod, but .fb packages, the `data`, `actors` etc. folders of the booster must end up in the same folder as the .fb packages.
  - Alternatively to adding .fb packages when the mod's already installed, you can find the required mod for the PC again and extract it into an empty folder (step 1) and continue at step 2 (extract the booster as explained above). After conversion, replace the unboosted .fb packages in the assets with the new, boosted ones.
  - IMPORTANT: Boosters for PC mods can be converted separately, no mod required. If the booster doesn't come with sounds and .igb assets are compatibele (or aren't included), the booster doesn't need any conversion at all.

Install Skins:
  - Follow the skin installation guide over [here](https://marvelmods.com/forum/index.php?msg=201703).
  - Instead of the game files (or MO2 mod folder), install the skins into the extracted mod's folders (e.g. actors, hud).

Convert Skins:
  1. Open the skin (from the extracted mod folder) in Finalizer.
  2. Add optimizations
     - For next-gen consoles and PC add `Convert igGeometryAttr to igGeometryAttr2`. This is also required for PSP, but it doesn't work (we don't know how at this time.) ![igGeometryAttr2](https://github.com/ak2yny/MUA-Mod-Converter/assets/92672223/73821bac-7844-4168-8934-123aee942c05)
     - If necessary, add the optimization `Convert images` (example configuration for PS3 below) ![configurationForPS3](https://github.com/ak2yny/MUA-Mod-Converter/assets/92672223/28431602-2c22-47e0-b66e-3a8627bc6e24)
     - Only if there is a normal map (DXT5 format) and only for PS3, add a text file with the name specified in the configuration (NormalMaps.txt in the screenshot above) to the same folder as the skin .igb file and add the normal map's texture name on a new line (just the name and extension). Other platforms need a different normal texture map or don't support normal maps at all.
     - Other optimizations might help, depending on the target platform and skin specifications.
  3. Run the optimizations.
  4. Save the file.
  5. Optionally, save the optimization set for future use.


## Known issues

  - Packages are converted using .xmlb extension, but mods usually include .engb files. Combat packages are fixed automatically, but non-combat packages aren't because they should only include certain files. The only .xml binary file included in the non-combat package should be the talents file, which is set-up in the cfgBuilder_info.cfg as .engb, so that shouldn't be a problem. It will be a problem if the non-combat package includes special .xml binary files.
  - Skins aren't converted because they can have normal texture maps, which require DXT5. Skins have to be manually converted, if necessary. (Step 2)
  - 6th generation console (and XML2 PC) conversions don't convert any IGB files at all, because the platforms don't support Alchemy 5 processes. Replace the IGB files with platform compatible assets. (Step 2)
  - Doesn't work in directories that require elevated (admin) permission (no matter if the user has these permissions or not).


## Credits

  - ak2yny for the batch script
  - BaconWizard17 for FB batch tool code and testing
  - Jayglass for discovering console requirements and testing
  - Lars for exploring sound mods on the Steam version
  - damarioculbreath for testing
