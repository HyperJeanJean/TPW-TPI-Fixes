# Collection of fixes for Theme Park World and Theme Park Inc

## Theme Park World

**DO NOT LAUNCH THE GAME UNTIL YOU HAVE COMPLETED ALL THE STEPS! OTHERWISE THE GAME WILL NOT WORK.**

 - If you had already installed the game: 
   - Backup your saves
   - Uninstall the game
   - Delete the installation folder (usually C:\Program Files (x86)\Bullfrog\Theme Park World)
   - Delete the corresponding folder in your VirtualStore if it exists (usually C:\Users\\\<Your username\>\AppData\Local\VirtualStore\Program Files (x86)\Bullfrog\Theme Park World)
   - Restart your computer

 - Install the game

 - Copy the following folders from your disc into your installation folder:
   - Data/Movies
   - Data/levels/fantasy/Music
   - Data/Levels/hallow/Music
   - Data/levels/jungle/Music
   - Data/levels/space/Music

 - Install the patch 2.0 (you can find it in the TPW folder)

 - Copy TP.exe, TP_AltRes.exe and the "data" folder from the "TPW" folder into your installation folder

 - Copy the files from the "Common" folder into your installation folder

 - Restart your computer

 - Optional: if you want to play with the bonus content from the Gold edition, copy the files from "TPW/Bonus content" into your installation folder

You can now launch the game. Remember to set your graphic settings to "high" and make sure the hardware renderer is enabled in the options for better graphics.

## Theme Park Inc

**DO NOT LAUNCH THE GAME UNTIL YOU HAVE COMPLETED ALL THE STEPS! OTHERWISE THE GAME WILL USE A FALLBACK FONT FOR MOST OF ITS IN-GAME TEXT.**

- If you had already installed the game: 
   - Backup your saves
   - Uninstall the game
   - Delete the installation folder (usually C:\Program Files (x86)\Bullfrog\Theme Park Inc)
   - Delete the corresponding folder in your VirtualStore if it exists (usually C:\Users\\\<Your username\>\AppData\Local\VirtualStore\Program Files (x86)\Bullfrog\Theme Park Inc)
   - Restart your computer

 - Install the game

 - Copy Game.exe, Game_AltRes.exe and the "data" folder from the "TPI" folder into your installation folder

 - Copy the files from the "Common" folder into your installation folder

 - Restart your computer

 - Optional: if you want to play with the bonus content from the North American version, copy the files from "TPI/Bonus content" into your installation folder

You can now launch the game. Remember to set your graphic settings to "high" and make sure the hardware renderer is enabled in the options for better graphics.

## Changing your resolution

The preferred way for changing your resolution is by editing the "data\Resolution.sam" file. By default, resolution is set at 1024x768 but you can change the number after "Res.RESOLUTION" to force the resolution you want. Please be aware though that increasing the resolution may have a negative impact on Theme Park World stability, and **WILL** have a negative impact on Theme Park Inc stability.

Here is a list of all resolutions for the standard executable:
 - 1 &rarr; 512x384
 - 2 &rarr; 640x480
 - 3 &rarr; 800x600
 - 4 &rarr; 1024x768
 - 5 &rarr; 1280x1024
 - 6 &rarr; 1600x1200
 - 7 &rarr; 2048x1536

Alternatively, you can use the "AltRes" executable (TP_AltRes.exe for TPW, Game_AltRes.exe for TPI) that provides a different set of resolutions, better suited for nowadays monitors:
 - 1 &rarr; 512x384
 - 2 &rarr; 640x480
 - 3 &rarr; 720x540
 - 4 &rarr; 960x720
 - 5 &rarr; 1440x1080
 - 6 &rarr; 1920x1440
 - 7 &rarr; 2880x2160

## Detailed list of changes

 - Fonts needed for both game have been extracted from their respective fonts.wad archive. TPW wouldn't work without them and TPI would work, but with a fallback font instead (Arial I believe). More info here: https://web.archive.org/web/20200628063012/https://www.adamhearn.co.uk/games/themeparkworld/tpwwin2kfix.html (although the fix provided on this website did not include all the font files)

 - The text now correctly appears on the park gates and the rides. To fix that, usp10.dll was renamed to usp11.dll as Windows seems to prefer using its own non-working version of usp10.dll

 - Both games executables have been fixed to avoid the issue where textures are replaced by white squares on large parks. This occured quite often in TPI and very rarely in TPW. From my understanding, this was caused by a miscalculation when the games estimate the amount of memory required if 32bit textures are enabled. This bug has been mitigated by the modification of a constant involved in the calculation to make the memory allocation estimation 8 times higher than normal.
   - For those who want to apply the fix themselves:
     - TPW: Replace `24 10 C1 E0 10` with `24 10 C1 E0 13` in TP.exe with a hex editor
     - TPI: Replace `24 0C C1 E7 10` with `24 0C C1 E7 13` in Game.exe with a hex editor

 - DDrawCompat is used to fix most of the graphic issues on modern systems

 - The bonus content from the North American versions are provided. Moreover, the two bonus rides for TPI have been fixed to work on non-english version of the game (the translations files were missing in the wad archive) although their name will be in english

 - Resolution will be forced to 1024x768 in both games as specified in "Data/Resolution.sam"

 - Alternate executables are provided with a different set of resolutions.
   - For those who want to change one of the resolution themselves:
     - TPW: With a hex editor, search for all occurences of `<32 bit integer for resolution width> C7 05 30 19 7A 00 <32 bit integer for resolution height>` (e.g. for 640x480: `80 02 00 00 C7 05 30 19 7A 00 E0 01 00 00`) in TP.exe and set the width and height to match your new resolution. If you use DDrawCompat, don't forget to add your new resolution in ddrawcompat.ini
     - TPI: With a hex editor, Search for all occurences of `<32 bit integer for resolution width> C7 05 C8 C8 A2 00 <32 bit integer for resolution height>` (e.g. for 640x480: `80 02 00 00 C7 05 C8 C8 A2 00 E0 01 00 00`) in Game.exe and set the width and height to match your new resolution. If you use DDrawCompat, don't forget to add your new resolution in ddrawcompat.ini

 - The file high.sam has been modified to make the game look a bit better. Anisotropic 16x is also enforced in DDrawCompat (see ddrawcompat.ini if you want to change that)

 - The QMixer DLL that is provided is a bit newer than the one distributed with the game. It seems to solve a few sound issues

 - The SFMAN32 DLL is provided in the "Unused" folder as the games executables have references to this DLL but AFAICT they don't appear to do anything with it

## Known issues
 - Random crashes. It may or may not be related to graphics settings. In TPI at least, having a resolution above 1024x768 makes the game really unstable.
 - Music archives in TPI are corrupted for the 2nd and 3rd parks, leading to music disappearing in the late game. Corrupted music tracks do not seem to be recoverable.
 - TPI does not handle non-ascii characters very well for prebuilt coasters  (e.g. the "é" character). Names are likely to be cut.
