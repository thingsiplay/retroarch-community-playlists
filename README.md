# RetroArch Community Playlists

## What is this?

Every RetroArch setup is highly customize able, which makes it difficult to
predict. Things such as file paths and names will most likely be different from
user to user. Therefore sharing custom playlists is almost impossible without
adapting them to their environment.

This repository is an attempt in streamlining this process a little bit. I
envision a place where community members can post or suggest their personal
playlist creations. The file paths in these collections are then reduced to its
minimum and changed to be consistent. This should make editing those files for
your own setup a bit easier.

### License

Everything shared on this place is given to the public domain with [The
Unlicense](LICENSE); it's just a playlist after all.

## How to import

### Download

First visit [RetroArch Community
Playlists](https://github.com/thingsiplay/retroarch-community-playlists) and click
the button `[ <> Code . ]`, which opens up a drop down menu. Click `[Download
ZIP]` . It should download all playlists now. Or alternatively, if you want,
just clone it with Git command:

```bash
git clone https://github.com/thingsiplay/retroarch-community-playlists
```

Now find the .lpl files in there, which are the playlists for RetroArch.

### First edit and adapt

The playlists are not usable in this form, because they contain placeholder you
have to replace. This is best done in bulk operation with specialized software.
Your editor most likely has some search and replace functionality.

The `"core_path": "DETECT"` in each game entry can stay as it is. This is
interpreted by RetroArch itself to use a default entry that is found on top of
the playlist file `"default_core_path": "..."` . Just leave the DETECT entries
and change the one default_core_path entry at the top. Same deal for
`"core_name"` .

You will encounter `$cores` and `$roms` . These represent placeholder, like
variables. This makes them easy to find and identify for automated replacement.

You also have to be careful with operating system specific things, which adds
extra spice to the already hot meal. File paths in Linux and similar systems
are noted with a slash `/` and on Windows its double backslash `\\` for each
directory segment (such as `gb/Super Mario Land.gb` vs `gb\\Super Mario
Land.gb` . And that's not all. File extension for cores in Linux is `.so`,
while `.dll` it is on Windows. It's true.

### Example before

Let's say we have these entries here:

```json
{
  "version": "1.5",
  "default_core_path": "$cores/fbneo_libretro.so",
  "default_core_name": "Arcade (FinalBurn Neo)",
  "label_display_mode": 0,
  "right_thumbnail_mode": 2,
  "left_thumbnail_mode": 0,
  "thumbnail_match_mode": 0,
  "sort_mode": 0,
  "items": [
    {
      "path": "$roms/fbneo/flagrall.zip",
      "label": "'96 Flag Rally",
      "core_path": "DETECT",
      "core_name": "DETECT",
      "crc32": "69F5767F|crc",
      "db_name": "FBNeo - Arcade Games.lpl"
    }
  ]
}
```

Steps to consider:

1. Change `$cores` to the location where the RetroArch cores are stored on your
   system. On my system it is `/home/tuncay/.config/retroarch/cores` .
2. Check the file ending of that core. For my system it is `.so` on Linux, for
   Windows it is `.dll` . So I leave it as it is.
3. Change `$roms/fbneo` to the location where your Genesis / Mega Drive Roms
   are located. For my system it is
   `/home/tuncay/Emulation/Roms/arcade/arcade_fbneo` .
4. Also make sure all these paths use the path separator of your operating
   system. For my Linux system it is just the slash `/` , like a website
   address. On Windows it is double backslash instead `\\` .
5. Important: Some playlists will have multiple different kind of Roms folders
   or systems they refer to. In example the same playlist could have `$roms/gb`
   and `$roms/gbc` , which are used by the same emulator. So replacing only one
   part would not be enough. Read the playlists README.md file in order to not
   miss that. For our example here we don't need to do that, as only one Roms
   directory source and only one core is used.

### Example after (Linux)

This is how it would look like on my machine:

```json
{
  "version": "1.5",
  "default_core_path": "/home/tuncay/.config/retroarch/cores/fbneo_libretro.so",
  "default_core_name": "Arcade (FinalBurn Neo)",
  "label_display_mode": 0,
  "right_thumbnail_mode": 2,
  "left_thumbnail_mode": 0,
  "thumbnail_match_mode": 0,
  "sort_mode": 0,
  "items": [
    {
      "path": "/home/tuncay/Emulation/Roms/arcade/arcade_fbneo/fbneo/flagrall.zip",
      "label": "'96 Flag Rally",
      "core_path": "DETECT",
      "core_name": "DETECT",
      "crc32": "69F5767F|crc",
      "db_name": "FBNeo - Arcade Games.lpl"
    }
  ]
}
```

### Example after (Windows)

This is how it could look like on your Windows machine:

```json
{
  "version": "1.5",
  "default_core_path": "E:\\PATH\\TO\\RETROARCH\\cores\\fbneo_libretro.dll",
  "default_core_name": "Arcade (FinalBurn Neo)",
  "label_display_mode": 0,
  "right_thumbnail_mode": 2,
  "left_thumbnail_mode": 0,
  "thumbnail_match_mode": 0,
  "sort_mode": 0,
  "items": [
    {
      "path": "E:\\PATH\\TO\\FBNEO\\ROMSET\\flagrall.zip",
      "label": "'96 Flag Rally",
      "core_path": "DETECT",
      "core_name": "DETECT",
      "crc32": "69F5767F|crc",
      "db_name": "FBNeo - Arcade Games.lpl"
    }
  ]
}
```

### Lastly install it

Now this is the easy part. If the playlist is done, just name it whatever you
want and put it in the playlist directory of your RetroArch folder. Done.

### Automate the import

This is where we are at, at the moment. My recommendation is to create small
scripts or any other way for automation of this process. I wrote a Python
script to help me with that at
[retroarch-import-playlist](https://github.com/thingsiplay/retroarch-import-playlist).
But it has an initial setup phase too, and an understanding of how commandline
tools work. So its not for everyone. Plus I am not 100% sure if it works on
Windows.
