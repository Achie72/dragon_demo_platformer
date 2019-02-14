# Dragondemo - Basic Documentation of objects, and functions  

This is a basic rundown on all functions and object, their members, parameters, and algorithm throughout the demo. As i'm still learning, there might be typos or not 100% accurate definitions. Check out the Pico-8 wiki also!

---
## Objects and their members
---
<a name="player"></a>
### Player - (Object)
- `player.x`: Marks the player `x` position in pixel metrics, not tiles.
- `player.y`: Marks the player `y` position in pixel metrics, not tiles.
- `player.jump`: Defines the jump force, that's going to apply on jumping.
- `player.ax`: Defines the player's acceleration on the `x` axis.
- `player.ay`: Defines the player's acceleration on the `y` axis.
- `player.acc`: Defines the acceleration force, with which the player speeds up from stading point.
- `player.frict`: Defines the friction, that is applied to the player, to slow him down after released movement.
- `player.mx_spd`: Defines the max speed, that the player can reach, applies to both directions for `player.ax`
- `player.max_fall` : Defines the maximum for the `player.ay`
- `player.facing`: Defines the last direction, the player faced. `0`: right, `1`: left.
- `player.grounded`: A boolean, to check if the player touched the ground, used for allowing jumps.
- `player.flowers`: Defines the number of the flowers, that the player collected. This is the main score, and will be tested on each level at the [`Princess`](#princess), to transit to the next level.
- `player.spr`: Contains the ID of the sprite, that is currently displayed for the player. his is the first element in that animation. The tilesheet contains two sprites for all animated objects.
- `player.walk_spr` : unused
- `player.jump_spr` : unused
- `player.hitSpr`: Contains the ID of the sprite, that is displayed if the player is damaged. This is the first element in that animation. The tilesheet contains two sprites for all animated objects.
- `player.life`: Defines the current health value, the player got. Can be decremented on colliding with enemies, and restored with [`Heart Flowers`](#heart_flower).
- `player.maxlife` :  Defines the maximum number of life, the player can obtain.
- `player.fireballs` : Defines the number of [`Fireballs`](#fireball) the player currently has.
- `player.key` : Defines the number of keys the player currently has.
- `player.invc`: Defines the number of frames, that is the player invincible for.
- `player.nextinvc`: Defines the next frame, where the player can be hit again. This is managed by the [`manage_internal_timers()`](#manage_internal_timers) function, according to the `player.invc` and the [`global.tick`](#global) values.
- `player.takenDamage`: Boolean to flag if the player recently received damage. Used by the animator that is responsible for rendering the `hitSpr` until the invincibility lasts. `0`: false, `1`: true.
- `player.win`: Boolean to check if the player has won the current level. `0`: false, `1`: true.
---
<a name="global"></a>
### Global - (Object)
I'm using the global object to store various members that i use all around the project, or they just contain game defining values.

- `global.gravity` : Defines the gravity value for all entities that are affected by the gravity.
- `global.camera_buffer`: Defines the buffer in which the camera doesn't move, if the player moves.
- `global.tick` : Defines a global timer, that ticks up every frame, and is handled by `ṁanage_interval_timers()` function. Used for all timings in the game.
- `global.debug` : Defines a debug value, that can be used to print out values during the gameplay, set by `set_ui()` function.
- `global.animation_queue` : Defines a collection of animation, that are played independently from the gameplay. At the moment used for animating `grass`, `fireflowers` and `death animations`.
---
### crect - (Object)
crect constantly stores the current colliding rectangle of the player. Defines with `(x1,y1)` and `(x2,y2)` points bounded rectangle. It can be easily printed, if the following line is commented back into the game in the `_draw()` function. (remove the `--` from before it):
 ```
 --rect(crect.x1,crect.y1,crect.x2,crect.y2,7)
 ```
---
<a name="fireballs"></a>
### fireballs - (Collection)
Is a simple collection, used for globally storing all the `fireballs` in the game.
<a name="fireball"></a>
* #### fireball - (Object)
The object, that defines the fireballs in the game. These projectiles can be acquired if the player picks up a `Fireflower`. Then `player.fireballs` is incremented by `2` and now the player can shoot forward moving projectiles, that die on wall collision, and kill enemies with one shot. The player can shoot by pressing the `X` button.

 - `fireball.x` : Defines the `x` position of the fireball in the game, given in pixel coordinates.
 - `fireball.y` : Defines the `y` position of the fireball in the game, given in pixel coordinates.
 - `fireball.spr` : Defines the ID of the starting sprite in the fireball's spritesheet- Currently it is made up by 4 sprites.
 - `fireball.speed` : Defines the movement speed of the firball on the `x` axis.
 - `fireball.direction` : Defines the direction the fireball is moving. `1` : right, `-1` : left. ID -> `44`
---
<a name="tall_grasses"></a>
### tall_grasses - (Collection)
A collection that is used to store all `grass` object in the game to help easier maintainability and animation for those objects.

<a name="grass"></a>
* #### grass - (Object)
Currently two grass objects are in the game, and they are differentiated by their sprite number. `64` : smaller version, `80` : taller.

 - `grass.x` : Defines the `x` position of the grass in the game, given in pixel coordinates.
 - `grass.y` : Defines the `y` position of the grass in the game, given in pixel coordinates.
 - `grass.spr` : Defines the ID of the starting sprite in the grass's spritesheet- Currently it is made up by 4 sprites. ID -> `Small : [64,67]` and `Tall : [80,83]`
---
<a name="fireflowers"></a>
### fireflowers - (Collection)
A collection that is used to store all `fireflower` object in the game to help easier maintainability and animation for those objects.

<a name="fireflower"></a>
* #### fireflower - (Object)
The fireflower object that the player needs to pick up to obtain fireball charges. If the player pick this up, then `player.fireballs` value that is greater than 0.
 - `fireflower.x` : Defines the `x` position of the fireflower in the game, given in pixel coordinates.
 - `fireflower.y` : Defines the `y` position of the fireflower in the game, given in pixel coordinates.
 - `fireflower.spr` : Defines the ID of the starting sprite in the fireflower's spritesheet- Currently it is made up by 4 sprites. ID -> `[96,99]`
---
<a name="camera"></a>
### Cam
Defines the camera that follows the player.
- `camera.x` : Defines the `x` position of the camera in the game, given in pixel coordinates.
- `camera.y` : Defines the `y` position of the camera in the game, given in pixel coordinates.
-`camera.speed` : Defines the scrolling speed of the camera.
---
<a name="enemies"></a>
### Enemies - (Collection)
A collection that is used to store all `enemies` object in the game to help easier maintainability and animation for those objects.

<a name="enemy"></a>
* #### Enemy - (Object)
Currently two enemy objects are in the game, and they are differentiated by their sprite, movement speed, and AI.
Can be constructed and automatically placed into it's collection by calling [`create_enemy()`](#create_enemy)

 - `enemy.x` : Defines the `x` position of the enemy in the game, given in pixel coordinates.
 - `enemy.y` : Defines the `y` position of the enemy in the game, given in pixel coordinates.
 - `enemy.defspeed` : Currently unused.
 - `enemy.speed` : Defines the movement speed of the enemy.
 - `enemy.ay` : Defines the velocity around the `y` Axis.
 - `enemy.spr` : Defines the ID of the starting sprite in the enemy's spritesheet- Currently it is made up by 2 sprites.
   - Knight: ID -> `[12,13]`
   - Spearman: ID -> `[28.29]`
 - `enemy.hitspr` : Defines the ID of the starting sprite in the enemy's hit animation spritesheet- Currently it is made up by 2 sprites.
   - Knight: ID -> `[12,13]`
   - Spearman: ID -> `[30,31]`
  - `type`: Defines the type of the enemy for the engine to recognize. `0` : Knight, `1` : Spearman.
  - `animspeed` : Defines the speed of the animations that the [`animate()`](#animate) renders for the object.

   **AI differences:**  
   Knights are faster, and walk of ledges, while spear-mans are slower, and the turn back on ledges, and do not fall down.
---
## Functions
---
<a name="create_enemy"></a>
### create_enemy(x,y,type)
A function for automatic [`enemy`](#enemies) creation and handling it into the global [`enemies`](#enemies) collection.

**Parameters:**  
- `x` - `[Number]` : Defining the `x` position for the enemy on the map in pixel coordinates.
- `y` - `[Number]` : Defining the `y` position for the enemy on the map in pixel coordinates.
- `type` - `[0,1]` : Defines the type of the enemy that is to be created. `0` : Knight, `1` : Spearman. (**See more: [enemy](#enemy)**)

The function basically checks for the `type` parameter, than creates a local `enemy` object, at the given `(x,y)` position. All other members are defined by the enemy's definition. (**See more: [enemy](#enemy)**)
After it, the function add the new object into the global [`enemies`](#enemies) collection.

**Example call:**
```lua
create_enemy(80,40,0)
-- creates a Knight at (80,40) in pixel coordinates (or (10,5) in tile coordinates)
```
---
<a name="create_grass"></a>
### create_grass(x,y)
A function for automatic [`grass`](#grass) creation and handling it into the global [`tall_grasses`](#tall_grasses) collection.

**Parameters:**  
- `x` - `[Number]` : Defining the `x` position for the grass on the map in pixel coordinates.
- `y` - `[Number]` : Defining the `y` position for the grass on the map in pixel coordinates.

The function basically randomizes an `rng` with the
```
rng = rnd(2) + 1
```
line, than creates a local `grass` object, at the given `(x,y)` position with the randomized ID. All other members are defined by the grass's definition. (**See more: [grass](#grass)**)
After it, the function add the new object into the global [`tall_grasses`](#tall_grasses) collection.

**Example call:**  
```lua
create_grass(80,40,0)
-- creates a grass at (80,40) in pixel coordinates (or (10,5) in tile coordinates)
```
---
<a name="create_animation"></a>
### create_animation(object,starting_frame,number_of_frames,speed,ticks,persistent,lifetime)
A function for creating and adding animation into the global `animation_queue` collection. (**See more: [animation_queue](#global)**)

**Parameters:**
- `obj` - `[Object with x and y members]`: Defining the object that the animation belongs to
- `starting_frame` - `[Number]` : Defining the ID of the starting frame in the animation.
- `number_of_frames` - `[Number]` : Defining the length of the animation in sprites, so a spritesheet animation containing 3 sprites has a 3 as the `number_of_frames`
- `speed` - `[Number]` : Defining the speed in which the animation plays.
- `tick` - `[Boolean]` : Defining the animation's orientation. `False` - rigth, `True` - left.  
- `persistent` - `[Boolean]` : Defining if the animation needs deleting after `lifetime` tick has passed. `True` : stays, `False` : deletion.
- `lifetime` - `[Number]` : Defining the number of frames the animation plays.

This function creates an animation with the given parameters, and passes it to the `global.animation_queue`. (**See more: [animate()](#animate)**)

**Example:**
```lua
create_animation(monster,monster.hitspr,2,30,false,false,10)
-- creates a sprite on the monster's position, starting from it's hitspr,
-- going for 2 sprite, 30 speed, looking left, and deletion after 10 frames.
```
---
<a name="create_fireballs"></a>
### create_fireball(x,y,direction)
A function for creating and adding [`fireballs`](#fireball) into the global [`fireballs`](#fireballs) collection.

**Parameters:**
- `x` - `[Number]` : Defining the `x` position for the fireball on the map in pixel coordinates.
- `y` - `[Number]` : Defining the `y` position for the fireball on the map in pixel coordinates.
- `direction` - `[-1,1]` : Defining the direction the fireball is moving. `1` : right, `-1` : left.

The function generates a local `fireball` object, at the given `(x,y)` position, heading into the `direction` defined direction. All other members are defined by the Fireballs's definition. (**See more: [fireball](#fireball)**) After creation it passes is into the global `fireballs` collection for later processing, and animating. (**See more: [move_fireball()](#move_fireball)**)

**Example:**
```lua
create_fireball(player.x+8,player.y,1)
-- creates a fireball right to the player, at it's y level, heading right
```
---
<a name="create_fireflower"></a>
### function create_fireflower(x,y)
A function for automatic [`fireflower`](#fireflower) creation and handling it into the global [`fireflowers`](#fireflowers) collection.

**Parameters:**  
- `x` - `[Number]` : Defining the `x` position for the fireflower on the map in pixel coordinates.
- `y` - `[Number]` : Defining the `y` position for the fireflower on the map in pixel coordinates.

The function creates a local `fireflower` object, at the given `(x,y)` and all other members are defined by the fireflower's definition. (**See more: [fireflower](#fireflower)**)
After the creation it passes it into the global [`fireflowers`](#fireflowers) collection for later processing and animating.

**Example call:**  
```lua
create_fireflower(80,40,0)
-- creates a create_fireflower at (80,40) in pixel coordinates (or (10,5) in tile coordinates)
```
