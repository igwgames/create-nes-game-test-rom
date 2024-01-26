# create-nes-game-test-rom

Test rom to make sure things like CI work with create-nes-game. Not actively used, but feel free to look at it as an example!

Otherwise, please take a look at [create-nes-game](https://create-nes-game.nes.science/), the main repository.

# How to compile

This rom uses [create-nes-game](https://create-nes-game.nes.science/) to build. Download a copy
of that to start.

## First time setup

1. Download [create-nes-game](https://create-nes-game.nes.science/), if you haven't already.
2. (Optional) Run `./create-nes-game install` to install the tool globally
3. Run `create-nes-game download-dependencies` to download dependencies of this game into this folder
4. Proceed to the next section to build the rom.

## Building the game

To build the rom, run `create-nes-game build` in the same directory as this readme file. 

You can run the game using the selected emulator (if available on your operating system) using the 
`create-nes-game run` command. Alternatively, the rom is available in the `rom/` folder.

## Running unit tests

This rom includes unit tests that can be used to verify that the game works. Run them using the 
`create-nes-game test` command. 

The tests are located in the `test/` folder.

# Directory layout

```
create-nes-game-test-rom
└─ config/                  - Configuration for the assembler/compiler
└─ graphics/                - Graphics data - backgrounds, palettes, and nametables
|    graphics.config.asm    - Add references to new graphics files here to use them from code
|    YOUR_FILE_NAME.chr     - Graphics data in binary form, such as exported from nesst
|                             Will automatically be run-length encoded into files with the .rle.chr suffix
|    YOUR_FILE_NAME.nam     - Nametable data in binary form, such as exported from nesst
|                             Will automatically be run-length encoded into files with the .rle.nam suffix
└─ rom/
|    YOUR_GAME.nes          - The game rom
|    YOUR_GAME.dbg          - Debugging information for the game - Mesen can use this to debug your code directly
└─ sound/
|    music.asm              - Music data, as exported from neslib's tool for music
|    sfx.asm                - Sound effect data, as exported from neslib's tool for sfx
└─ source/
|    assembly/              - Runtime information to support the C engine. Can also contain custom code
|    c/                     - Most game code lives here
|        main.c             - Entrypoint for the game
|        system-defines.h   - Constants and symbols commonly used in nes development
|        mapper.h           - Helpers for working with the rom's mapper
└─ temp/                    - Temporary storage for the compiler. Usually safe to ignore
└─ test/                    - Test files for the game, written in javascript. Uses nes-test
└─ tools/                   - Compile and emulation tools required by the game, downloaded by nes-test
```

# NESLib 

This rom uses multiple tools from [Shiru](https://shiru.untergrund.net/) - namely neslib and famitone2. You can find the 
details on [Shiru's website](https://shiru.untergrund.net/). The readme files are probably the best reference.

It was also bundled with music and sound effects from Shiru's game 
[LAN Master](https://shiru.untergrund.net) - which have likely been replaced with the game's own assets.


## Sound Effects

Sound effects should be created using [famitracker](http://famitracker.com) (Version 0.4.6). They should be exported
as an NSF file, and stored in `sound/sfx.nsf`. The tool will automatically convert them using famitone2's tools. 

How to do this, from famitracker:
1. In the `File` menu, select `Create NSF`.
2. Toward the middle of the dialog, there is a `Type of file` dropdown - choose `NSF - Nintendo Sound File`
3. Save the generated file into the `sound/` folder as `sfx.nsf`.

Next time you run `create-nes-game build` your new sound effects will be added to the game.

## Music

Music is created using [Famitracker 0.4.6](http://famitracker.com/). Once you have music you like, you'll need to
export it for use with this engine. Follow these steps to do so: 

1. In the `File` menu, select `Export Text`
2. Save the generated file into the `sound/` folder as `music.txt`

Next time you run `create-nes-game build` your new music will be added to the game.

-----

This rom uses [create-nes-game](https://create-nes-game.nes.science/)!
