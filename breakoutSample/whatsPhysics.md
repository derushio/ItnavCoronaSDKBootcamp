# 3. Physics is ...

## Physics is ...
CoronaSDK's characteristic system is physics engine. (For example physics engine can emulate the movement of a bouncing ball.)
You can use the physics engine from this code.

```lua
-- Load the function to use the physics engine and put it in `physics` .
physics = require("physics")
-- Activate physics engine
physics.start(true)
physics.setGravity(0, 0)
```
There is no action on the app at this point of coding, but there will be from next chapter.

from
CoronaSDK Reference [physics]

[https://docs.coronalabs.com/api/library/physics/index](https://docs.coronalabs.com/api/library/physics/index.html)

---

## All code in this chapter
All code in this chapter

```lua
-----------------------------------------------------------------------------------------
--
-- Let's make Breakout
-- main.lua
--
-----------------------------------------------------------------------------------------



-- ############################## What is variable？ ##############################

-- `width` contains the width(1080) of the display
width = display.contentWidth
-- `height` contains the height(1920) of the display
height = display.contentHeight

-- display group(necassary to draw the display with coronaSDK)
displayGroup = display.newGroup()

-- ############################## What is variable？ ##############################



-- ############################## physics is ... ##############################

-- Load the function to use the physics engine and put it in `physics` .
physics = require("physics")
-- Activate physics engine
physics.start(true)
physics.setGravity(0, 0)

-- ############################## physics is ... ##############################


```
Display should show the same as the following image.<br />
Still same view of the previous chapter.

![](./image/execBreakoutSample2.png)
