BlueMSX Wii

Written by Tim Brugman	
Last Updated: V1.0.3: 13 February 2015 
(http://www.wiimsx.com)

## FEATURE LIST
* Powerful and accurate BlueMSX emulator core featuring:
  * Very accurate emulation of MSX, MSX2, MSX2+, Turbo-R.
  * Very accurate emulation of all sound processors; PSG, SCC, MSX-Music, MSX-Audio and Moonsound.
  * Multiple machine definitions, easily adaptable/extensible.
  * Build-in ROM database to automatically use the right ROM mapper for megaROM games.
  * A lot more, see BlueMSX website.
* Wii improvement regarding emulation:
  * 100% smooth video emulation because of synchronization between MSX and Wii video output.
  * 100% smooth audio because of automatically calibrating re-sampling.
  * PAL Wii video output switches automatically between 50Hz/60Hz to meet the video output standard of the MSX.
* Powerful GUI:
  * Game selector with multiple directory support.
  * Shows two screenshots for every game.
  * Screenshots can be automatically added by creating screenshot from ‘home’-menu.
  * Games can easily be added/configured by editing .xml files.
  * State can be saved/restored from the ‘home’-menu.
  * Restore state menu shows the date/time and a screenshot of the saved state.
  * On-screen keyboard by pointing your wiimote to the screen.
* General features:
  * Automatic SD-Card installation procedure, runs out of the box.
  * Two controllers supported for multiplayer games.
  * Classic controller supported (highly recommended!).
  * USB keyboard supported (Logictech wireless Wii keyboard recommended).

## ADDING GAMES
Originally written by Maikel Bloemendal

BlueMSX-wii needs a directory structure on your SD-card. Games are stored under SD:/MSX/Games/

In this folder, there should be a dirlist.xml OR gamelist.xml, only one of these files may be present.

    The contents of dirlist.xml

as an example, I will take the contents of the dirlist in the gamepack which is installed with the application
```
<DirectoryList>
  <Item Name="MSX1 Demos" Directory="MSX1Demos"/>
  <Item Name="MSX2 Demos" Directory="MSX2Demos"/>
  <Item Name="Remakes" Directory="Remakes"/>
  <Item Name="MSXDev '08" Directory="MSXDev08"/>
  <Item Name="MSX Machines" Directory="Machines"/>
</DirectoryList>
```
The "Name" items specify the name as shown in the emulator, the Directory is the directory on the SD-card. Please keep in mind that the filesystem on the wii is case sensitive, and thus these need to be specified correctly.

Each directory can have other dirlist.xml files.

Example gamelist.xml:
```
<GameList>
  <Game Title="01 Deep Dungeon">
    <CommandLine>/machineMSX /rom1 msxdev08.zip /rom1zip 01-DDUNGEON.ROM</CommandLine>
    <ScreenShot>01-DDUNGEON-1.png</ScreenShot>
    <ScreenShot>01-DDUNGEON-2.png</ScreenShot>
  </Game>
  <Game Title="02 I Need Speed">
  <CommandLine>/machine MSX /rom1 msxdev08.zip /rom1zip 02-ineedspeed.rom</CommandLine>
    <Settings KeyboardJoystick="true"/>
    <ScreenShot>02-ineedspeed-1.png</ScreenShot>
    <ScreenShot>02-ineedspeed-2.png</ScreenShot>
  </Game>
</GameList>
```
A game element should always specify the Title, which is the name that is shown in the emulator.

### Commandline

The CommandLine specifies settings to start the emulator, it basically specifies the machine, disks, roms and cassettes.
It is possible to specify the following:
```
/machine MSX
/machine MSX2
/machine MSX2+
/machine "MSX2 - No Moonsound" (default)
/machine MSXturboR
```
These machines are the most commonly used machines, the MSX and MSX2 are european, MSX2+ is japanese
It is possible to supply any machine available in the SD:/MSX/Machines/ folder.
NOTE1: Filenames with spaces need to be double quoted, otherwise the XML file is invalid
NOTE2: Default machine is without moonsound because it adds noticable loading time. If a game supports moonsound, use /machine MSX2.

To load roms:
```
/rom1 file.zip or file. (rom, ri, mx1, mx2, col, sg, sc)
/rom1zip file.rom (necessary when you have multiple rom files in your zip, makes it possible to disk-change using a hotkey (default key = F11))
/romtype1 name (most of the romtypes are autodetected, if it is not working you need to specify the romtype, see list of romtypes below)
/rom2
/rom2zip
/romtype2
```
To load disks:
```
/diskA file.zip or file. (dsk, di1, di2, 360, 720, Sf7)
/diskAzip (necessary when you have multiple rom files in your zip, makes it possible to disk-change using a hotkey (default key = F11))
/diskB
/diskBzip
```
To load cassettes:
```
/cas file.zip or file.cas
/caszip
```
To make things extra clear, an example:
```
/machine MSX2 /diskA Magnar.zip /diskAzip Magnar-1.dsk
```

### Settings

The Settings element can only have the attribute KeyboardJoystick="true", to map WiiMote 1 as keyboard control and WiiMote 2 as joystick 1. More about this mapping can be found in the guide "Customizing controller buttons"

### KeyMap

Not shown, but also possible is a KeyMap element, to customize the controller buttons, read the guide "Customizing controller buttons" for more information.

### Screenshot

The Screenshot elements specify which screenshots are shown when the game is selected in the emulator. The maximum number of screenshots specified is 2. Screenshots can be generated via the home-menu, when running the games.
For these screenshots, there must be a folder named "Screenshots" (don't forget the capital).

<details>
<summary>supported romtypes</summary>

Megaroms:
"ASCII16"
"ASCII16SRAM2"
"ASCII8"
"ASCII8SRAM8"
"KoeiSRAM8"
"KoeiSRAM32"
"Konami"
"KonamiSCC"
"Manbow2"
"MegaFlashRomScc"
"Halnote"
"HarryFox"
"Playball"
"HolyQuran"
"CrossBlaim"
"Zemina80in1"
"Zemina90in1"
"Zemina126in1"
"Wizardry"
"GameMaster2"
"SuperLodeRunner"
"R-Type"
"Majutsushi"
"Synthesizer"
"KeyboardMaster"
"GenericKonami"
"SuperPierrot"
"WordPro"
"Normal"
"MatraInk"
"NettouYakyuu"

System roms:
"Bunsetsu"
"CasPatch"
"Coleco"
"MegaCart"
"SG1000"
"SC3000"
"SG1000Castle"
"SegaBasic"
"FMPAC"
"FMPAK"
"DiskPatch"
"Jisyo"
"Kanji1"
"Kanji12"
"MB8877A"
"SVI738FDC"
"TC8566AF"
"TC8566AFTR"
"WD2793"
"Microsol"
"MoonSound"
"SunriseIDE"
"BeerIDE"
"GIDE"
"GoudaSCSI"
"NMS1210"
"fsa1fm2"
"FSA1FM2"
"Panasonic8"
"PanasonicDram"
"PanasonicWx16"
"Panasonic16"
"Panasonic32"
"A1FMModem"
"fsa1fm1"
"FSA1FM1"
"Standard16K"
"SVI328CART"
"SVI80COL"
"SVI727"
"SVI738FDC"
"MSX-AUDIO"
"MSX-MUSIC"
"National"
"CX5M-MUSIC"
"VMX80"
"HBI-V1"
"SFG-01"
"SFG-05"
"NET"
"SF-7000IPL"
"FMDAS"
"Obsonet"
"Dumas"
"NoWind"

SG-1000 roms:
"sg1000castle"
</details>

<details>
<summary>unsupported romtypes</summary>

"0x4000"
"0xC000"
"auto"
"basic"
"mirrored"
"forteII"
"msxdos2"
"konami5"
"konami4"
"ascii8"
"halnote"
"konamisynth"
"kbdmaster"
"majutsushi"
"ascii16"
"gamemaster2"
"ascii8sram"
"koei"
"ascii16sram"
"konami4nf"
"ascii16nf"
"snatcher"
"sdsnatcher"
"sccmirrored"
"sccexpanded"
"scc"
"sccplus"
"scc-i"
"scc+"
"pac"
"fmpac"
"fmpak"
"rtype"
"crossblaim"
"harryfox"
"loderunner"
"korean80"
"korean90"
"korean126"
"holyquran"
"coleco"
"sg1000"
"castle"
</details>

## CUSTOMIZING CONTROLLER BUTTONS
Written by Maikel Bloemendal

As current keyboard layouts and the WiiMote, Nunchuck and classic controller buttons are different from the keys and buttons of the MSX, some keys have a different function than they used to have.

As far as it is possible, all keys will be the same.
There are some differences:
F6-F10: current keyboards have F1-F12, the MSX only has F1-F5, F6-F10 map to the buttons that are on the same place, which are: Select, Stop, Clr home, Insert and Delete.
F11 is mapped to quick-change disk (an emulator feature).
F12 is mapped to the 'home' button of the controller to make the GUI fully controllable using the USB keyboard.

WiiMote buttons A and 2 are mapped to MSX button 1
WiiMote buttons B and 1 are mapped to MSX button 2
The nunchuck button Z maps to button A (of the WiiMote)
The nunchuck button C maps to button B (of the WiiMote)

It is possible to make a custom keymapping for each game.
This is done in the gamelist.xml files, which can be found in the /MSX/Games folders
by supplying a <KeyMap> element.

Supplying the <KeyMap KeyboardJoystick="true"/> will result in the following mapping:
WiiMote 1 will map to keyboard:
Button A and 2 to space
Button B and 1 will be unmapped
The direction arrows go to the corresponding directions on the keyboard

WiiMote 2 will map to joystick 1
Button A and 2 to MSX Button 1
Button B and 1 to MSX Button 2
The direction arrows go to the corresponding directions of joystick 1

It is possible to make a different keymapping for each key.
A custom keymapping example:
<KeyMap buttonA1="space" button11="left" button21="right"/>

### List of names/values for the buttons (these are the values BEFORE the '=')

#### WiiMote 1 buttons:
"up1"
"down1"
"left1"
"right1"
"buttonA1"
"buttonB1"
"button11"
"button21"
"home1"
"plus1"
"minus1"
#### Classic controller 1 buttons:
"buttonX1"
"buttonY1"
"buttonL1"
"buttonR1"
"buttonZL1"
"buttonZR1"

#### WiiMote 2 buttons:
"up2"
"down2"
"left2"
"right2"
"buttonA2"
"buttonB2"
"button12"
"button22"
"home2"
"plus2"
"minus2"
#### Classic controller 2 buttons:
"buttonX2"
"buttonY2"
"buttonL2"
"buttonR2"
"buttonZL2"
"buttonZR2"

#### USB keyboard keys:

NOTE: Since revision r123 (not release V1.0) the names of the numbers, keypad buttons and symbols are changed, the old names are not described in this guide anymore, because they are unusable in V1.0!
direction: "up", "down", "left", "right"
letters (must be lowercase): "a" - "z"
Numbers: "key_0" - "key_9"
Keypad buttons (are in brackets): "num_0" - "num_9", "num_period", "num_slash",  "num_asterisk", "num_minus", "num_plus", except for "num_enter" and "num_equals"
Function keys (also lowercase): "f1" - "f12"
Symbols: "exclamation", "doublequote", "hash", "dollar", "percent", "ampersand", "quote", "open_parenthesis", "close_parenthesis", "asterisk", "plus", "comma", "minus", "period", "slash", "colon", "semicolon", "less", "equal", "greater", "question", "at", "open_bracket", "backslash", "close_bracket", "caret", "underscore", "backquote", "open_brace", "vertical_bar", "close_brace", "tilde"
Other characters: "space", "return", "backspace", "tab", "escape", "insert", "delete", "home", "end", "page_up", "page_down"

### List of actions to which the keys can be mapped (quoted values AFTER the '=')

#### MSX Joystick 1 buttons:
"joy1-up"
"joy1-down"
"joy1-left"
"joy1-right"
"joy1-button1"
"joy1-button2"
"joy1-button3"
"joy1-button4"
"joy1-button5"
"joy1-button6"

#### MSX Joystick 2 buttons:
"joy2-up"
"joy2-down"
"joy2-left"
"joy2-right"
"joy2-button1"
"joy2-button2"
"joy2-button3"
"joy2-button4"
"joy2-button5"
"joy2-button6"

#### MSX Keyboard keys:

Direction keys: "up", "down", "left", "right"
Letters (should be lowercase): "a" - "z"
Nnumbers: "0" - "9"
Keypad: "num0" - "num9", "numperiod", "numdiv", "nummul", "numsub", "numadd" and "numcomma"
Function keys (also lowercase): "f1" - "f5"
Special keys: "stop", "cls", "select", "ins", "del"
Symbols: "neg", "circomflex", "backslash", "at", "leftbracket", "semicolon", "colon", "rightbracket", "comma", "period", "div", "underscore", "graph", "torikeshi", "space", "jikkou"
Other keys: "esc", "backspace", "tab", "return", "ctrl", "leftshift", "rightshift", "caps", "code", "pause", "print"

ColecoVision keys: "coleco1-0", "coleco1-1", "coleco1-2", "coleco1-3", "coleco1-4", "coleco1-5", "coleco1-6", "coleco1-7", "coleco1-8", "coleco1-9", "coleco1-star", "coleco1-hashmark", "coleco2-0", "coleco2-1", "coleco2-2", "coleco2-3", "coleco2-4", "coleco2-5", "coleco2-6", "coleco2-7", "coleco2-8", "coleco2-9", "coleco2-star", "coleco2-hashmark"

#### Hotkey functions:
"hotkey_quit"
"hotkey_fdc_timing"
"hotkey_sprite_enable"
"hotkey_msx_audio_switch"
"hotkey_front_switch"
"hotkey_pause_switch"
"hotkey_wave_capture"
"hotkey_screen_capture"
"hotkey_load_state"
"hotkey_save_state"
"hotkey_card_remove_1"
"hotkey_card_remove_2"
"hotkey_card_auto_reset"
"hotkey_disk_change"
"hotkey_disk_remove_a"
"hotkey_disk_remove_b"
"hotkey_disk_auto_reset"
"hotkey_cas_rewind"
"hotkey_cas_remove"
"hotkey_cas_read_only"
"hotkey_cas_auto_rewind"
"hotkey_cas_save"
"hotkey_emu_pause"
"hotkey_emu_stop"
"hotkey_emu_speed_normal"
"hotkey_emu_speed_increase"
"hotkey_emu_speed_decrease"
"hotkey_emu_max_speed"
"hotkey_emu_reset_soft"
"hotkey_emu_reset_hard"
"hotkey_emu_reset_clean"
"hotkey_volume_increase"
"hotkey_volume_decrease"
"hotkey_mute"
"hotkey_stereo"
"hotkey_window_size_normal"
"hotkey_window_size_fullscreen"
"hotkey_fullscreen_toggle"

## CHANGELOG

V1.0.3

* Fixed USB keyboard that did not work anymore in V1.0.2
* Added USB 2.0 support (when running IOS58). It now is possible to install on fast USB 2.0 storage device (which can de faster than an SD-Card).
* Updated libogc package to r4264.

V1.0.2

* Updated devkitPPC (R21) and libogc (1.8.3)
* Fixed vertical offset bug on NTSC wiis.
* Fixed glitches in sound playback.
* Improved audio, pause instead of hick on changing disks.
* Reduced average audio lag from 85ms to 21ms, about the same as video lag now.
* Greatly improved audio frequency stability.
* Fixed issue with button mapping introduced in V1.0.1.
* Gui coordinate fixes, not correctly centered since V1.0.1.
* Small update in build-in gamepack.

V1.0.1

* Fixed display problem (black screen) on some Wii's, more accurate scaling/centering on all Wii's.
* Key mapping of numeric keys does not work
* Feature: Make buttons of different controllers separately mappable

V1.0

* Updated to BlueMSX V2.8.2.
* Added full support for GameCube controller.
* Fixed problems with 'save state'. Also improved speed of saving a lot.
* Allow empty screenshot elements in gamelist.xml files (did crash before).
* Missing 'Screenshots' sub directories are now automatically created (on generating screenshot).
* Solved showing wrong day of state files.
* Embedded game pack will only be installed when no game pack is already installed.

V1.0RC

* First public release
