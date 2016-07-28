# MACVENTURE File extraction

Welcome!

This repo contains various tutorials describing how to extract the files for ICOM's MacVenture games, starting from [Zojoi's re-release](http://www.zojoi.com/shadowgate_macventure/) of these games.

For now, this tutorial covers:

- How to extract the files from the Windows executables (.exe) game files, to be used with [the WebVenture engine](https://github.com/mrkite/webventure) ([Linux](#linux), [Windows]()).
- How to decompose these newly extracted files to use them with [ScummVM's](http://scummvm.org) [MacVenture implementation](https://github.com/blorente/scummvm/tree/macventure) (This is still unstable and a Work In Progress) ([Linux and Windows]()).

## Prerequisites

I will assume that you own and have a legal copy of the desired game's executable (e.g., shadowgate.exe) or installable (e.g. shadowgate.msi)

## Extracting disk files

This section deals with extracting the .dsk (Mac versions) and .2mg (Apple II versions) images from the executables. These can be plugged directly into the WebVenture emulator.

NOTE: This approach doesn't work for the files of Uninvited. Somehow the game is newer, and thus the resource files look different.

### Linux

- Navigate to the folder containing the .msi istaller.
- Install it with `wine`. Usually this can be accomplished by right-clicking and executing the .msi with wine.
- Navigate to the folder where wine installed the executable. In my case, `~/.wine/drive_c/Program Files(x86)/MacVenture Series/`
- Locate the target executable file, and open it with the archive manager. This should allow you to see the .rsrc folder, along with the .data and .text files.
- Navigate inside the `.rsrc/256` folder, and locate the two resources with a big size. They are usually named `1011` and `1012`, and they are about 810 KB big. The first one is the Apple II game, and the second one is the Macintosh game.
- (Optional) To check that these are the correct files, you can open them with a hex editor (GHex), and if there is no JavaScript code and they are not image files, you are in the money!
- Extract the desired resource file and rename it to <gamename>.dsk/2mg, depeding on what you extracted.
- Profit!

### Windows

- Install the game using the .msi installer.
- Locate the installed .exe file.
- Utilize a resource-extracting tool (like [Resource Hacker](http://www.angusj.com/resourcehacker/)) to locate the resources mentioned in the previous section.
- Copy the entire content of the resource file (Right Click -> Select All -> Copy should suffice).
- Paste them into a hex editor (I recommedn [HxD](https://mh-nexus.de/en/hxd/)).
- Save the document from the text editor with the appropriate name and extension (e.g. "Shadowgate.dsk").

### Playing with WebVenture

The WebVenture emulator is fully JavaScript-based, and therefore there is little to do to play with teh games:

- Clone the github repository: https://github.com/mrkite/webventure
- Paste the extracted .dsk or .2mg file into the root folder of the cloned repo.
- Utilize a server utility to create a localhost server. I use python's built-in one `$> python -m http.server 8080` (I use python3, no guarrantee that this will work with other versions).
- Open a browser, navigate to the server address (`localhost:8080` in my case) and enjoy!
