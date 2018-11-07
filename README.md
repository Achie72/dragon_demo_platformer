# pico8
PICO-8 Fooling and Learning

Generally this repository will contain my learning and experiments about the fantasy console named PICO-8.

## Dragondemo.p8
My first ever project, in which i try to implement a basic platformer, with movements, and collisions as usual. Still under development, and heavily WIP.  
Currentyl i'm not concerned about token numbers, in this project i want to focus on readability.

### Current Features
* Tile based collision check
* Global, configurable animator
* Simple camera, that follows player
* Fully dynamic UI prints. Just add the element you want to the `ui` collection in `set_ui()` and watch the magic happen.
* Changeable player skins. Press `x` ingame to change your skin.
* Pickups in the form of flowers. Also pickup sounds.

[Animator based on this cartridge](https://www.lexaloffle.com/bbs/?tid=3115 "Simple Animation Function")  
[Collision based on this article](http://gamedev.docrobs.co.uk/first-steps-in-pico-8-easy-collisions-with-map-tiles "First Steps in PICO-8: Easy Collisions with Map Tiles")

## How to use this
* Open PICO-8 and type in `folder`. The OS will open the cartridge directory, with your dedicated file browser.
* Paste `dragondemo.p8` into the directory.
* Return to PICO-8 and press `ctrl+r` to reload.
* Type `load dragondemo.p8` and `run`.

## Examples i used
You can find them under `examples/`. Credit to all owners. You can find their name and original cartridge name in the .p8 files. Thanks for them for sharing them.

Credit to all examples:
* coin thief adventure! - dylan
* advanced micro platformer - matthughson
* pixel-perfect collision test - josh millard
* simple-collision-function - Scathe
