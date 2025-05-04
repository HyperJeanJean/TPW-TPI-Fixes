# Collection of fixes for Theme Park World and Theme Park Inc

## Theme Park World

 - Install the game

 - Copy the following folders from your disc into your installation folder:
   - Data/Movies
   - Data/levels/fantasy/Music
   - Data/Levels/hallow/Music
   - Data/levels/jungle/Music
   - Data/levels/space/Music

 - Install the patch 2.0 (you can find it in the TPW folder)

 - Copy the TP.exe file from the "TPW" folder into your installation folder

 - Copy the files from the "Fixes" folder into your installation folder

 - Restart your computer

 - Optional: if you want to play with the bonus content from the Gold edition, copy the files from "TPW/Bonus content" into your installation folder

 - Optional: if you want to play on a 1080p monitor, you can copy the files from "TPW/1440x1080" into your installation folder, but be warned that this may have a negative impact on the game stability

## Theme Park Inc

 - Install the game

 - Copy the Game.exe file from the "TPI" folder into your installation folder

 - Copy the files from the "Fixes" folder into your installation folder

 - Restart your computer

 - Optional: if you want to play with the bonus content from the North American version, copy the files from "TPI/Bonus content" into your installation folder

 - Optional: if you want to play on a 1080p monitor, you can copy the files from "TPI/1440x1080" into your installation folder, but be warned that this **WILL** have a negative impact on the game stability

## Detailed list of changes

 - TPW now works on modern systems thanks to the inclusion of some missing font files (in the folder "data/tpwfnt"). More info here: https://web.archive.org/web/20200628063012/https://www.adamhearn.co.uk/games/themeparkworld/tpwwin2kfix.html

 - The text now correctly appears on the park gates and the rides. To fix that, usp10.dll was renamed to usp11.dll as Windows seems to prefer using its own non-working version of usp10.dll

 - Both games executables have been fixed to avoid the issue where textures are replaced by white squares on large parks. This occured quite often in TPI and very rarely in TPW. From my understanding, this was caused by a miscalculation when the games estimate the amount of memory required if 32bit textures are enabled. This bug has been mitigated by the modification of a constant involved in the calculation to make the memory allocation estimation 8 times higher than normal.
   - For those who want to apply the fix themselves:
     - TPW: Replace `24 10 C1 E0 10` with `24 10 C1 E0 13` in TP.exe with a hex editor
     - TPI: Replace `24 0C C1 E7 10` with `24 0C C1 E7 13` in Game.exe with a hex editor

 - DDrawCompat is used to fix most of the graphic issues on modern systems

 - The bonus content from the North American versions are provided. Moreover, the two bonus rides for TPI have been fixed to work on non-english version of the game (the translations files were missing in the wad archive) although their name will be in english

 - Resolution will be forced to 1024x768 in both games as specified in "Data/Resolution.sam" (if you use the 1440x1080 files it will be 1440x1080)

 - The file high.sam has been modified to make the game look a bit better. Anisotropic 16x is also enforced in DDrawCompat (see ddrawcompat.ini if you want to change that)

 - The QMixer DLL that is provided is a bit newer than the one distributed with the game. It seems to solve a few sound issues

 - The SFMAN32 DLL is provided in the "Unused" folder as the games executables have references to this DLL but AFAICT they don't appear to do anything with it

## Known issues
 - Random crashes. It may or may not be related to graphics settings. In TPI at least, having a resolution above 1024x768 makes the game really unstable.
 - Music archives in TPI are corrupted for the 2nd and 3rd parks, leading to music disappearing in the late game. Corrupted music tracks do not seem to be recoverable.
