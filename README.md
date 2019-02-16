# pico8
PICO-8 Fooling and Learning

Generally this repository will contain my learning and experiments about the fantasy console named PICO-8.  
Don't forget to check the people i mentioned in the `Examples and credits` part.

## Dragondemo.p8
My first ever project, in which i try to implement a basic platformer, with movements, and collisions as usual. Still under development, and heavily WIP.  
Currently i'm not concerned about token numbers, in this project i want to focus on readability.

### Current Features
* Tile based collision check
* Global, configurable animator
* Simple camera, that follows player
* Fully dynamic UI prints. Just add the element you want to the `ui` collection in `set_ui()` and watch the magic happen.
* Changeable player skins. Press `x` ingame to change your skin.
* Pickups in the form of flowers. Also pickup sounds.
* Proper health system. You start with three, indicated on the GUI, you lose one if you collide with enemies.
* GUI containing health, and picked up flowers, and missing ones.
* Two enemy AI. `knight` who just wanders, and turns if he can't go forward, and falls down on ledges. `spearman` who will guard the position, and won't fall of edges.
* Proper game loop. Now you can lose, and win, and restart the game if one or the other happens.
* Damage indication in the form of red flashing, invincibility frames, and health pickups in the form of the heart flowers.
* The ability for the player to stomp enemies upon landing on them, and gaining upward momentum from them.
* An OOP-like method for creating enemies, and animated grasses onto the game. `create_enemy` and `create_grass`


[Animator based on this cartridge](https://www.lexaloffle.com/bbs/?tid=3115 "Simple Animation Function")  
[Collision based on this article](http://gamedev.docrobs.co.uk/first-steps-in-pico-8-easy-collisions-with-map-tiles "First Steps in PICO-8: Easy Collisions with Map Tiles")

## How to use this
* Open PICO-8 and type in `folder`. The OS will open the cartridge directory, with your dedicated file browser.
* Paste `dragondemo.p8` into the directory.
* Return to PICO-8 and press `ctrl+r` to reload.
* Type `load dragondemo.p8` and `run`.

Alternatively you can try it on [my](https://achie72.github.io/pico8/) github page.

## Examples and credits
You can find them under `examples/`. Credit to all owners. You can find their name and original cartridge name in the .p8 files. Thanks for them for sharing them.

Credit to all examples:
* coin thief adventure! - dylan
* advanced micro platformer - matthughson
* pixel-perfect collision test - josh millard
* simple-collision-function - Scathe

Thanks for:  
* enargy on Discord, for helping me with the collision system remake
* tobiasvl on Discord, for putting up with my shit with lua ternaries

The whole family on Pico-8 Discord
