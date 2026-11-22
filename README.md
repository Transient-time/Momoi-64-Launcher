# Momoi64 Launcher

A Windows app for joining Super Momoi 64 co-op sessions. It replaces the manual pack swap from the [join guide](https://rentry.org/moi64): you paste the host's post, click Download on the pages it opens, and press Play.

The launcher handles the steps the guide makes you do by hand:

- comparing the post's links with what is installed, and skipping packs whose link has not changed
- picking finished zips up from your Downloads folder
- deleting the old version of each pack and unzipping the new version into the game's `mods` folder
- clearing the game's `.tmp` folder and `mod.cache`, so the game does not download the packs again while joining
- starting the game

## First run

1. Get `Moi64Launcher.exe`, or build it from source (see the last section).
2. Start it, press **Add game...** and pick the game's `.exe`, for example `64 Player Build.exe`. Every game `.exe` in that folder shows up in the list at the top. A launcher placed inside the game folder adds the game on its own.
3. If a pink **ROM missing** bar shows, press **Choose ROM...** on it and pick your own Super Mario 64 (US) ROM. The launcher checks the file and copies it to where the game looks. It does not download ROMs. The bar uses the game's own search: an unmodified US ROM saved as a `.z64` file under any name, in the data folder or next to the game's `.exe`, counts as in place.

**Settings** in the top right holds the things you need once or rarely: **Edit game...** changes a game's folder, its data folder (normally `%APPDATA%\sm64coopdx`) and its launch options, and the same list has **Add game...**, the two **Open folder** commands, **Clear game cache** and **Options...**. Hovering over the game picker shows the game's paths.

## Every session

The three numbered buttons under the headline are the three steps. The blue one is the step to take next, and a finished step gets a tick.

1. Copy the host's post from the thread, at least the lines with pack links.
2. Press **1 Paste post**, press Ctrl+V, or drag the text onto the window.
3. Press **2 Get packs**. Your browser opens the download page of every pack you are missing.
4. Click **Download** on each page. The launcher installs each file as soon as the download finishes. When a file name does not say which pack it is (the romhack often arrives as `mods.zip`), the launcher asks once and remembers the answer.
5. When the headline says **Ready to play**, press **3 Play**. In the game: Join, then Public Lobby.

A zip you already have goes in through the **...** button on the pack's row, then **Choose zip...**, or by dragging the zip onto the row.

**Show activity** at the bottom of the window opens the full list of what the launcher did; the newest line shows next to it.

## Changes on your computer

- In the game's `mods` folder, the launcher deletes only mods it installed. The list of those mods lives in `moi64-launcher.json` in the game folder.
- When a pack brings a mod with the same name as a mod you installed by hand, your copy moves to a dated folder such as `moi64-backup\2026-11-14_193003` in the game folder. The launcher does not delete those copies. After the first run on an install set up by hand, the backup folder can hold a few hundred MB of old packs; delete it once the game runs fine.
- In the game's data folder, the launcher deletes `.tmp`, the older `tmp` folder and `mod.cache`. Saves, settings, the ROM and your own mods there stay as they are. A folder without `sm64config.txt`, `mod.cache` or `baserom.us.z64` in it gets left alone completely.
- In Downloads, the launcher looks only at files that appear after you press Get packs, and moves a zip out only once it knows which pack the zip is.
- The launcher keeps its settings in `%APPDATA%\Moi64Launcher\settings.json` and holds pack zips in `%LOCALAPPDATA%\Moi64Launcher\packs`. A held zip gets deleted once every game folder you set up has the pack, unless **Keep pack zips** is ticked in Options.
- While the game runs, the launcher leaves packs and the cache as they are, and finishes once you close the game.

## Downloads from gofile

gofile blocks downloads by programs on free accounts. The site signs every request with a secret key that gofile changes regularly, and a request signed with an old key gets the sender's IP address banned. A workaround would break often and could get players banned, so the launcher opens the page and your browser does the download.

For hosts: a pack posted as a plain link to a `.zip` file (a GitHub release file, for example) downloads with no clicking. Keep one pack per line as `Name: link`. Posting the same link again for an unchanged pack lets everyone skip that download.

## Troubleshooting

- Joining gets stuck, or the game downloads packs in-game: close the game, then pick **Settings**, **Clear game cache**. After a join where the game downloaded mods from the host, a pink line under the pack list says how many; hovering over the line lists them. Usually that is a pack whose link changed since your last paste.
- A pack row turns red: the row says why, for example "has no mods in it" after the wrong zip downloaded, or "Drive C has 131 MB free; this pack needs 215 MB". Press **Retry** on the row to try that pack again. A pack that stopped for lack of disk space installs from the zip the launcher already holds, so free up space first and nothing downloads again. On a red row, **Open page** and **Choose zip...** sit in the row's **...** list. The `moi64-backup` folder in the game folder is the first place to look for space (see Changes on your computer).

## Limits

- Windows 10 (version 1803 or later) or Windows 11. Both include the .NET Framework version the launcher needs.
- The launcher does not download the game itself. The game build is linked from the [join guide](https://rentry.org/moi64).
- Joining the lobby stays a few clicks in the game, because the game has no launch option for joining a lobby.
- The file and folder pickers (Browse..., Choose zip...) are Windows' own and follow your Windows theme.
