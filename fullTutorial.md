### @activities true

# Making a Platformer Game Part One

## Introduction
### Introduction @unplugged

Welcome to part one of this this tutorial on how to make a platformer game with Arcade MakeCode.
In this tutorial we will cover the basics of how to:

* Create a Player character
* Move the Player element around the screen
* Create a Game Space using platforms using the tilemap tool
* Add Food to collect using the tilemap tool

We will also cover the following Coding Concepts [(more info here)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions).

* [Variables](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#variables)
* [User Input Events](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#input-event)
* [Listener Events](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#change-listener)
* [Logic](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#logic)
* [Loops](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#loops)

## Introduction Creating your Player Character
### Create your Character @fullscreen

To create your character. Drag the  ``||variables:set mySprite||`` ``||sprites:to IMAGE of kind Player||`` into the ``||loops:on start||`` block.
Click on the blank square and choose a player from the Gallery. What about a duck?
Anything in the ``||loops:on start||``  block runs when the game starts.

***Coding Concept Used***: In this step we have created a [Variable (click here to find out more)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#variables)

```blocks
let mySprite = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . b 5 5 b . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . b b b b b 5 5 5 5 5 5 5 b . .
    . b d 5 b 5 5 5 5 5 5 5 5 b . .
    . . b 5 5 b 5 d 1 f 5 d 4 f . .
    . . b d 5 5 b 1 f f 5 4 4 c . .
    b b d b 5 5 5 d f b 4 4 4 4 b .
    b d d c d 5 5 b 5 4 4 4 4 4 4 b
    c d d d c c b 5 5 5 5 5 5 5 b .
    c b d d d d d 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
```

## Moving your Character
### Move your Character left and right @fullscreen

Drag ``||controller:moveSprite with buttons||`` under your existing block.
Click on the plus sign at the end of the block. Keep ``||controller:vx||`` as 100 but change the  ``||controller:vy||`` setting to 0.

```blocks
let mySprite = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . b 5 5 b . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . b b b b b 5 5 5 5 5 5 5 b . .
    . b d 5 b 5 5 5 5 5 5 5 5 b . .
    . . b 5 5 b 5 d 1 f 5 d 4 f . .
    . . b d 5 5 b 1 f f 5 4 4 c . .
    b b d b 5 5 5 d f b 4 4 4 4 b .
    b d d c d 5 5 b 5 4 4 4 4 4 4 b
    c d d d c c b 5 5 5 5 5 5 5 b .
    c b d d d d d 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
controller.moveSprite(mySprite, 100, 0)
```

### Make our Character Jump @fullscreen

Let's add a **Jump Event** which listens for the ``||controllers:A button||`` being pressed.
When that happens it will move our character up in the y axis. Up here is a negative value. Drag in the ``||controllers: on A button pressed ||``
Drag inside that a block ``||sprites:set mySprite x to 0 ||``. Change ``||sprites:x||`` to ``||sprites:vy velocity||`` set it to **-150**

***Coding Concept Used***: In this step we have created a [Input Event (click here to find out more)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#input-event)

```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    mySprite.vy = -150
})
```

## Change the colour of the background

### Change the colour of the background @fullscreen
Change the colour of your background. Drag in from scene ``||scene:set background color to ||`` after your current blocks and click on the square to choose a colour.

```block
scene.setBackgroundColor(9)
```

## What about Gravity?
### What happens? @fullscreen
When we press ``||controllers:A||`` (which is SPACE on the keyboard) we jump but we don't come back down.
We need gravity! Add another block like ``||sprites:set mySprite x to 0 ||`` to the on start block and change the property to
``||sprites: ay (acceleration y) ||`` and set that to **300**

```blocks
let mySprite: Sprite = null
mySprite = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . b 5 5 b . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . b b b b b 5 5 5 5 5 5 5 b . .
    . b d 5 b 5 5 5 5 5 5 5 5 b . .
    . . b 5 5 b 5 d 1 f 5 d 4 f . .
    . . b d 5 5 b 1 f f 5 4 4 c . .
    b b d b 5 5 5 d f b 4 4 4 4 b .
    b d d c d 5 5 b 5 4 4 4 4 4 4 b
    c d d d c c b 5 5 5 5 5 5 5 b .
    c b d d d d d 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
controller.moveSprite(mySprite, 100, 0)
mySprite.ay = 300
```
## Using Tilemaps
### Create a Floor using a Tilemap @fullscreen
Oh no, with gravity we fall off of the bottom of the scree. To make a platformer we are going to need a floor and some platforms.
Drag in the ``||scene:set tilemap to  ||`` block into your on start block.

***Coding Concept Used***: The tilemap is a kind of [Array (click here to find out more)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#arrays)

```blocks
let mySprite: Sprite = null
mySprite = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . b 5 5 b . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . b b b b b 5 5 5 5 5 5 5 b . .
    . b d 5 b 5 5 5 5 5 5 5 5 b . .
    . . b 5 5 b 5 d 1 f 5 d 4 f . .
    . . b d 5 5 b 1 f f 5 4 4 c . .
    b b d b 5 5 5 d f b 4 4 4 4 b .
    b d d c d 5 5 b 5 4 4 4 4 4 4 b
    c d d d c c b 5 5 5 5 5 5 5 b .
    c b d d d d d 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
controller.moveSprite(mySprite, 100, 0)
mySprite.ay = 200
tiles.setTilemap(tiles.createTilemap(
            hex`100008000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,myTiles.tile2],
            TileScale.Sixteen
        ))

```

### Create a Floor using a Tilemap 2 @fullscreen

Click on the square and this opens up the ``||scene:Tilemap||`` editor.
Change the size in the bottom left to **10 x 8**  because each tile is 16 pixels square this is the just a bit bigger than the size of the screen.
The whole screen is actually **160px wide by 120px high**. You can do the maths if you want :)

![Change size to 10 by 8 ](https://raw.githubusercontent.com/mickfuzz/getting-started-making-a-platformer-test1/master/images/tilemap_1.png)

###Create a Floor using a Tilemap 3 @fullscreen
Create a line of tiles to be a floor. Choose a suitable tile for your floor. Why not the first, default one. Draw a line by clicking tiles at the bottom of the drawing area to create a floor.
Now select the **Wall Drawing tool** and click the same squares. Then click on Done.

![Create a row of images and walls ](https://raw.githubusercontent.com/mickfuzz/getting-started-making-a-platformer-test1/master/images/makecode-1-2020-02-14-145027.gif)

### Now draw more platforms @fullscreen

Now you will fall and come to rest on the floor. Can also jump up. In fact you can jump a lot, **even when you are in the air!**
We'll fix that in a bit.  For now **add some more platforms in your tilemap.**

![Design your platforms ](https://raw.githubusercontent.com/mickfuzz/getting-started-making-a-platformer-test1/master/images/makecode-2.png)

## Jump only when touching floor
### Jump only when touching floor @fullscreen

To jump only when touching floor we need to add in an extra ``||logic:logic if||`` block in our Event block.
Drag in a ``||logic:if true then||`` block from the Logic section ``||ControllerButtonEvent: on A button pressed ||``.



```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (true) {
    	mySprite.vy = -150
    }
})
```

### Jump only when touching floor @fullscreen
Drag in a ``||scene:Scene||`` block ``||scene:is mySprite hitting wall ||`` inside the ``||logic:logic if||`` block. Change the setting to ``||scene:hitting wall bottom||``.
Now the player will only jump when it is touching down on a platform.  

***Coding Concept Used***: To decide if the player is touching the ground we
use  [Logic (click here to find out more)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#logic)

```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (mySprite.isHittingTile(CollisionDirection.Bottom)) {
        mySprite.vy = -150
    }

```

## Add a Goal - Collectable Food

### Adding Food to our Tilemap @fullscreen
**Now we need a Goal for our Game**.
To add Food for the Player to collect **click on the tilemap image and add in a few yellow squares**.
In the next step we will then turn them into strawberries.

![Add in Yellow Squares ](https://raw.githubusercontent.com/mickfuzz/getting-started-making-a-platformer-test1/master/images/makecode-yellow-s1-2020-02-16-19.gif)

### Adding Food: Change Squares to Food @fullscreen
Drag a ``||loops: for element value of list||`` block after your current blocks.
Replace ``||variables:list||`` with ``||scene: array of all locations||`` and choose a yellow block. Inside the ``||for loop||`` add a ``||variables:set strawberry to sprite of kind Food||`` and add a strawberry image from the gallery.
After this add a ``||scene:place on top of ||`` block and set to ``||scene:place strawberry on top of value||``

![Convert Yellow Squares ](https://raw.githubusercontent.com/mickfuzz/getting-started-making-a-platformer-test1/master/images/makecode-yellow-s2.gif)

### Adding Food: Change Squares to Food @fullscreen

Let's removing the original yellow square which is now behind the strawberry by adding a ``||scene:scene||`` block  ``||scene: set blank box at||``  into our loop.
Keep the blank image in the first part of the block but change the second value to ``||variables:value||``.


***Coding Concept Used***: We add to the tilemap which is a kind of [Array](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#arrays) - and then we use a [Loop](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#loops) to loop through all the
elements of the array and turn each one into a different kind of game component.

![blank square](https://github.com/mickfuzz/makecode-platformer-101/blob/master/images/loop_replace_yellow.png?raw=true)



## Eating Food and Points
### Eating Food and Points  @fullscreen
Drag in a ``||sprites:on sprite of kind Player overlaps ||`` block anywhere on your workspace.
Change the second ``||variables:Player||`` variable to ``||variables:Food||``.

***Coding Concept Used***: This code listens out of the condition of a Player touching any Food items and then makes
and event happen so we call it a [Listener Event](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#change-listener)

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
})
```

### Eating Food and Points 2 @fullscreen
Drag in a ``||sprites:destroy mySprite ||`` block inside the ``||sprites:on sprite of kind Player overlaps ||`` block
Grab the ``||variables:otherSprite||`` variable from the first block onto the ``||variables:mySprite||`` part of the ``||sprites:destroy||`` block



```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy()
})
```

### Eating Food and Points 3  @fullscreen
Add an ``||info:Info||`` block ``||info:change score by 1||`` under the ``||sprites:destroy||`` block
Now Your food should disappear when you touch it and you **gain points**.
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeScoreBy(1)
})
```
***Coding Concept Used***: In this step we use the built in score [Variable (click here to find out more)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#variables)

### Check your code

Check your code too see if it matches the image in the tool tip

```blocks
namespace SpriteKind {
    export const Door = SpriteKind.create()
}
namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
}
let strawberry: Sprite = null
let mySprite: Sprite = null
mySprite = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . b 5 5 b . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . b b b b b 5 5 5 5 5 5 5 b . .
    . b d 5 b 5 5 5 5 5 5 5 5 b . .
    . . b 5 5 b 5 d 1 f 5 d 4 f . .
    . . b d 5 5 b 1 f f 5 4 4 c . .
    b b d b 5 5 5 d f b 4 4 4 4 b .
    b d d c d 5 5 b 5 4 4 4 4 4 4 b
    c d d d c c b 5 5 5 5 5 5 5 b .
    c b d d d d d 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
controller.moveSprite(mySprite, 100, 0)
mySprite.ay = 200
tiles.setTilemap(tiles.createTilemap(
            hex`0a0008000000000000000000000000000300000000000300010101030000000001010000010100000000000000000000000003000003000000000000010101010000000000000000000001010101010101010101`,
            img`
                . . . . . . . . . .
                . . . . . . . . . .
                2 2 2 . . . . . 2 2
                . . 2 2 . . . . . .
                . . . . . . . . . .
                . . . . . . 2 2 2 2
                . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1],
            TileScale.Sixteen
        ))
scene.setBackgroundColor(9)
for (let value of tiles.getTilesByType(myTiles.tile1)) {
    strawberry = sprites.create(img`
        . . . . . . . 6 . . . . . . . .
        . . . . . . 8 6 6 . . . 6 8 . .
        . . . e e e 8 8 6 6 . 6 7 8 . .
        . . e 2 2 2 2 e 8 6 6 7 6 . . .
        . e 2 2 4 4 2 7 7 7 7 7 8 6 . .
        . e 2 4 4 2 6 7 7 7 6 7 6 8 8 .
        e 2 4 5 2 2 6 7 7 6 2 7 7 6 . .
        e 2 4 4 2 2 6 7 6 2 2 6 7 7 6 .
        e 2 4 2 2 2 6 6 2 2 2 e 7 7 6 .
        e 2 4 2 2 4 2 2 2 4 2 2 e 7 6 .
        e 2 4 2 2 2 2 2 2 2 2 2 e c 6 .
        e 2 2 2 2 2 2 2 4 e 2 e e c . .
        e e 2 e 2 2 4 2 2 e e e c . . .
        e e e e 2 e 2 2 e e e c . . . .
        e e e 2 e e c e c c c . . . . .
        . c c c c c c c . . . . . . . .
    `, SpriteKind.Food)
    tiles.placeOnTile(strawberry, value)
    tiles.setTileAt(value, myTiles.tile0)
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeScoreBy(1)
})
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (mySprite.isHittingTile(CollisionDirection.Bottom)) {
        mySprite.vy = -150
    }
})
```

![blank square](https://github.com/mickfuzz/makecode-platformer-101/blob/master/images/code_complete_mca.png?raw=true)

## Play Part One
### Play Part One @unplugged

**That's it now let's play our game**

Then play your game to test that it works ok.

Is it too easy? If so, can you make it changes that so one of the jumps is more challenging?
Or is it too hard? If so what can you change to make it easier?

Try making small or large changes to the following:

* the jump ``||sprites:vy (velocity y)||``  in the ``||controller:on A button pressed||`` block
* player gravity with the ``||sprites:ay (acceleration y)||`` setting
* player speed left and right in the ``||controller:move mySprite with buttons||`` block
* the location of the platforms to make the jumps more challenging

Get a friend or family member to test it out. Can they collect all the Food first time?
Getting the balance right between too hard and too easy is key to making our game challening and interesting to play.

Hope you enjoyed part one of this tutorial. We built a simple game and also met
 the following [Coding Concepts](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions).

* [Variables](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#variables)
* [User Input Events](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#input-event)
* [Listener Events](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#change-listener)
* [Logic](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#logic)
* [Loops](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#loops)

In part two we add the following elements to our platform game.

* Adding an End Goal that you must touch to win game
* Make it so you much collect all Food to win the game
* Creating a larger Game Space by increasing the width of the level
* Adding Levels to extend our Game Space and increase challenge

## Making a Platformer Game Part Two

### Getting Started @unplugged

This is part to of our tutorial on making a Platformer Game. Part One is here.
In the next screen you will have the relevant blocks to start with.

 In part two we add the following elements to our platform game.

* Adding an end goal that you must touch to win game
* Make it so you must collect all Food to win game
* Creating a larger Game Space
* Adding Levels
* Adding a Timer

We will also cover the following Coding Concepts [(more info here)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions).

* [Arrays](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#arrays)
* [Functions](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#functions)
* [Logic](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#logic)


## Adding a End Door

### Adding a End Goal 1 @fullscreen

Have a look at our starting blocks. We can see ``||controller:Controls||`` our that move our Player and allows them to jump.
A Platform design and location of Food in our ``||scene:tilemap||``. A ``||loops:loop||`` that creates our food. Finally a ``||sprites:On Event||`` listener removes the food when our player touches it.  

### Adding a End Goal @fullscreen

Next we add an **End Goal**. When you hit this block you will win (or go to the next level).
Click on the ``||scene:tilemap||`` image and add a brown square where you want your **End goal / Door** to another level to be.
![door in tilemap](https://github.com/mickfuzz/makecode-platformer-101/blob/master/images/door_2.png?raw=true)

### Adding a End Door 2 @fullscreen

To save time we will copy the **Code Pattern** used to create our Food blocks. Let's duplicate that whole ``||loops:for element value ||`` loop by right clicking it and selecting **Duplicate.**

![blank square](https://github.com/mickfuzz/makecode-platformer-101/blob/master/images/loop_door.png?raw=true)

### Adding a End Door 3 @fullscreen

Drag the duplicated ``||loops:for element||`` loop back into your ``||loops:on Start||`` loop under that previous one.
Change the ``||scene:locations||`` colour block to brown, change the name to ``||variables:chest||``, the image to a chest and the ``||sprites: of kind||`` value to ``||sprites:Door||``.
As ``||sprites:Door||`` isn't in the drop-down list, click on **Add new Kind** and enter Door there.  

***Coding Concept Used***: We add to the tilemap which is a kind of [Array](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#arrays) - and then we use a [Loop](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#loops) to loop through all the
elements of the array and turn each one into a different kind of game component.

![Door loop ](https://github.com/mickfuzz/makecode-platformer-101/blob/master/images/door_3.png?raw=true)

### Adding a End Door 4 @fullscreen
Add a ``||sprites:on sprite of kind Player overlaps ||`` block anywhere on your workspace.
Change the second ``||sprites:Player||`` variable to ``||sprites:Door||``.

***Coding Concept Used***: This code listens out of the condition and then makes
and event happen so we call it a [Listener Event](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#change-listener)


```blocks
namespace SpriteKind {
    export const Door = SpriteKind.create()
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Door, function (sprite, otherSprite) {
})
```


### Adding a End Door 5 @fullscreen
Drag in a ``||game: gameOver  ||`` block inside the ``||sprites:on sprite of kind Player overlaps ||`` block and set it to ``||game:game over WIN||``

```blocks
namespace SpriteKind {
    export const Door = SpriteKind.create()
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Door, function (sprite, otherSprite) {
    game.over(true)
})
```
## You must Collect all Fruit  
### You must Collect all Fruit 1  @fullscreen
Let's add **challenge** to the game so you must collect all food before you can end the game.
Drag a Logic block ``||logic:if true then||`` inside the ``||sprites:on sprite of kind Player overlaps of kind Door ||``.
In the new ``||logic:if true then||`` block replace ``||logic:true||`` with a ``||logic:0 = 0 ||`` block from Logic section.

```blocks
namespace SpriteKind {
    export const Door = SpriteKind.create()
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Door, function (sprite, otherSprite) {
    if (0 == 0) {
        game.over(true)
    }
})
```

### You must Collect all Fruit 2 @fullscreen
We need new blocks to do with lists called arrays. To find them type **array** in the search box and press Enter.
Replace the first **0** in the``||logic:0 = 0 ||`` with an ``||arrays:length of array list||`` block.
![array image search](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/all_food_1.png)

### You must Collect all Fruit 2 @fullscreen

Drag the larger ``||variable:set sprite list to array of kind Player||`` into the workspace.
Then replace ``||variable:list||`` in the ``||arrays:length of array ||`` with a ``||sprites:array of kind Player||`` block.
Then change  ``||sprites:array of kind Player||`` to ``||sprites:array of kind Food||``

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Door, function (sprite, otherSprite) {
    if (sprites.allOfKind(SpriteKind.Food).length == 0) {
        game.over(true)
    }
})
```
## Increase the Game Space   
### Increase the Game Space 1 @fullscreen
More **challenge**. Let's increase the Game Space to create a scrolling game.
First let's make our **Player** start on the left of the screen.
Drag in a ``||sprites:set mySprite position to x 10 y 100 ||`` under the block setting ``||sprites:acceleration y||``
![game space one](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/game_size_1.png)

### Increase the Game Space 2 @fullscreen
Under that block another one under Scene that says ``||scene:camera follow sprite mySprite||``
![game space one](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/game_size_3.png)

### Increase the Game Space 3 @fullscreen
This new position already gives an idea of the direction of travel. Now click on your ``||scene:tilemap||`` image and change the size to **20 x 8** .
Click **Done** and add in new blocks for platforms and food to fill in the new space.
Remember to add in Walls using the **Wall Tool**.
![game space one](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/game_size_2.png)


## Adding another Level  
### Adding another Level 1 @fullscreen

To add another level we are going to move some of our code out of the on start block so we can run it more than once.
Create a new ``||functions:Function||`` by clicking on the **Advanced** tab on our toolbar, then  ``||functions:Functions||``
And then click **Make a Function**. Enter createLevels in the white box.
![game level one](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/new_level_1.png)

### Adding another Level 2 @fullscreen
Move the new function next to the bottom part of your ``||loops:on start||`` loop.
Then move the two ``||loops: for element value||`` loops into the ``||functions: createLevels||`` function.
Right click and select **Format Code**. Then drag in the ``||functions:call createLevels||`` from ``||functions:Functions||`` to the end of the ``||loops:on start||`` loop.

![game level two](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/makecode-function-levels1.gif)

### Adding another Level 3 @fullscreen
Under ``||variables:variables||`` make a new variable called level. Then drag the ``||variables: set level to 0||``
block towards the end of your on start block but before the ``||functions:call createLevels||`` block.
![game level three](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/new_level_3.png)

### Adding another Level 4 @fullscreen
Create a new ``||functions:Function||`` by clicking on the **Advanced** tab on our toolbar, then  ``||functions:Functions||``
And then click **Make a Function**. Enter chooseLevel in the white box.


```blocks
function chooseLevel () {
}
```

### Adding another Level 5 @fullscreen
Drag only the  ``||scene:set tilemap to||`` into the new ``||functions:chooseLevel||`` function by holding down **Control** on your Keyboard while you drag the block.
Right click and select **Format Code** to make the screen tidy.
```blocks
namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
function chooseLevel () {
    tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000030000000000000400030000000000030000000101000000000000010101030000000001010000000000000000000300000101000000000000000000000000000101010000000000000300000300000000030000000000000000000000010101010000000001010000000000000000000000000000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . 2 2 . . . . . .
                2 2 2 . . . . . 2 2 . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . 2 2 2
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . 2 2 2 2 . . . . 2 2 . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
}
```

### Adding another Level 6 @fullscreen
Drag in the ``||functions:call chooseLevel||`` from ``||functions:Functions||`` to the end of the begining of the ``||functions:createLevel||`` function.

***Coding Concept Used***: In these past steps we have created a
 [Function (find out more here)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#functions)

![game level four](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/new_level_4.png)

### Adding another Level 7 @fullscreen
Now add a Logic block ``||logic:if true then||`` inside the ``||sprites:chooseLevel ||`` block
Move the the ``||scene:set tilemap to||``  inside the logic block.
In the new ``||logic:if true then||`` block replace ``||logic:true||`` with at ``||logic:0 = 0 ||`` block from Logic section.

```blocks
namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
function chooseLevel () {
    if (level == 0) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000030000000000000400030000000000030000000101000000000000010101030000000001010000000000000000000300000101000000000000000000000000000101010000000000000300000300000000030000000000000000000000010101010000000001010000000000000000000000000000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . 2 2 . . . . . .
                2 2 2 . . . . . 2 2 . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . 2 2 2
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . 2 2 2 2 . . . . 2 2 . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
}
```

### Adding another Level 8 @fullscreen
Right click on the Logic block ``||logic:if level = 0 ||`` and duplicate it.
Change 0 to 1 in the second block and drag it back into the ``||functions:chooseLevel||`` function.

***Coding Concept Used***: To decide what level to create we
use  [Logic (click here to find out more)](https://mickfuzz.github.io/makecode-platformer-101/learningDimensions#logic)

```blocks
namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
function chooseLevel () {
    if (level == 0) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000030000000000000400030000000000030000000101000000000000010101030000000001010000000000000000000300000101000000000000000000000000000101010000000000000300000300000000030000000000000000000000010101010000000001010000000000000000000000000000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . 2 2 . . . . . .
                2 2 2 . . . . . 2 2 . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . 2 2 2
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . 2 2 2 2 . . . . 2 2 . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
    if (level == 1) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000030000000000000400030000000000030000000101000000000000010101030000000001010000000000000000000300000101000000000000000000000000000101010000000000000300000300000000030000000000000000000000010101010000000001010000000000000000000000000000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . 2 2 . . . . . .
                2 2 2 . . . . . 2 2 . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . 2 2 2
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . 2 2 2 2 . . . . 2 2 . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
}
```

### Adding another Level 9 @fullscreen
Repeat the process again  changing the ``||varaiables:level||`` number  to two.
Move your ``||game:game over||`` win block into and delete the ``||scene:tilemap||`` block.  

```blocks
namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
function chooseLevel () {
    if (level == 0) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000030000000000000400030000000000030000000101000000000000010101030000000001010000000000000000000300000101000000000000000000000000000101010000000000000300000300000000030000000000000000000000010101010000000001010000000000000000000000000000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . 2 2 . . . . . .
                2 2 2 . . . . . 2 2 . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . 2 2 2
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . 2 2 2 2 . . . . 2 2 . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
    if (level == 1) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000030000000000000400030000000000030000000101000000000000010101030000000001010000000000000000000300000101000000000000000000000000000101010000000000000300000300000000030000000000000000000000010101010000000001010000000000000000000000000000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . 2 2 . . . . . .
                2 2 2 . . . . . 2 2 . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . 2 2 2
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . 2 2 2 2 . . . . 2 2 . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
    if (level == 2) {
        game.over(true)
    }
}
```

### Adding another Level 10 @fullscreen
In the ``||sprites:on sprite of kind Player overlaps Door ||`` event block add a ``||variables:change level by 1||`` block.
Next add a ``||sprites:set mySprite position to x 10 y 100 ||``
Then add a ``||functions:createLevels||`` block from ``||functions:Functions||``

![game level four](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/new_level_4.png)

## Add a Timer
### Add a Timer @fullscreen

To add more **challenge** to our game the final thing we will do is add a timer for each level.
Drag from ``||info:Info||`` a ``||info:start countdown ||`` block to the start of the ``||functions:createLevels||`` function.

![game timer](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-101/master/images/timer_1.png)


## End Notes
### End Notes @unplugged

**Congratulations - Now Play your Game**

Then play your game to test that it works ok. And get someone else to test it too.

Is it too easy? Or is it too hard? If so what can you change to make it easier or harder?
Try making small or large changes to the following:

* Location of the **Platforms** and your **Food** and **End Goal**
* **Game Space** size
* **Timer** settings
* Number of **Food** items

Now you have the core of your game in place you can add more to it.
How about the following

* Add Enemies
* Add Moving Enemies
* Add Music and Sound Effects
* Add Animations to make your Player come alive
* Double Jump
* Add instructions and comments
* Jump on Enemies to zap them

There are follow-up tutorials to come but for the meantime just have a play.
