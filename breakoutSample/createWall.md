# 4. Create walls

## Draw background image
You can draw the background by this code.

```lua
-- A black color background is lonesome, so let's add a image to the background
background = display.newImageRect(displayGroup, "bg_space.png", width, height)
background.x = width/2
background.y = height/2
```

from：CoronaSDK Reference [newImageRect]

[https://docs.coronalabs.com/api/library/display/newImageRect
](https://docs.coronalabs.com/api/library/display/newImageRect.html)

---

## Draw walls
Let's create walls so the moving ball will bounce inside of the display.<br />
Walls should have 4 sides. You can create each of them by using `display.newLine(LeftTop's X coordinate, LeftTop's Y coordinate, RightBottom's X coordinate, RightBottom's Y coordinate)`<br />
<br />
However, 4 walls created like<br />
`walls1 = display.newLine(displayGroup, 0, 0, width, 0)`<br />
`walls2 = display.newLine(displayGroup, 0, 0, 0, height)`<br />
...<br />
doesn't look neat.<br />
<br />
So, let's try using a table system.<br />
Table is defined `walls = {}`, and you can access variable by `walls[0]`, `walls[1]`.<br />
Also, variable value should be defined as `tag`. It will make it easier for you to recognize which wall by tagging them.<br />

```lua
以下のコードを書き、壁を描画してみましょう。 
-- Let's create an associative array of walls
walls = {}
walls[1] = display.newLine(displayGroup, 0, 0, width, 0)
walls[1].tag = "topWall"

walls[2] = display.newLine(displayGroup, 0, 0, 0, height)
walls[2].tag = "leftWall"

walls[3] = display.newLine(displayGroup, width, 0, width, height)
walls[3].tag = "rightWall"

walls[4] = display.newLine(displayGroup, 0, height, width, height)
walls[4].tag = "bottomWall"
```

from<br />
CoronaSDK Reference [newLine]

[https://docs.coronalabs.com/api/library/display/newLine](https://docs.coronalabs.com/api/library/display/newLine.html)

---

## Setting the walls in a lump by using `for statement`
You can batch process an array by using `for statement`.
`for statement` is written `for i = initial value, last value, How many i are added each time do ~ end`.
Each time the i value get's added up towords the last value, inside of `do ~ end` will be continuously executed. It will stop when it hits the last value.
Let's create walls by `for statement`.
  
By using `physics.addBody(what you are registering, type, option)` you can register to the physics system. The types are "static" objects that don't move, and "dynamic" objects that do move. Objects moves with "kinematic" as well, but since objects moves along gravity with "dynamic", objects moves without relation to gravity with "kinematic".
Try writing the following code.

```lua
-- for i = initial value, end value(is included), How many i are added each time do ~ end
-- `#` is the number of elements
for i = 1, #walls, 1 do
    -- Change the wall thickness
    walls[i].strokeWidth = 50
    -- `physics.addBody(what you are registering, type, option)` Register to the  physics system
    physics.addBody(walls[i], "static", {density = 0.0, friction = 0.0, bounce = 1.0})
end
```

Reference
CoronaSDK Reference[addBody]

[https://docs.coronalabs.com/api/library/physics/addBody](https://docs.coronalabs.com/api/library/physics/addBody.html)

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



-- ############################## Create walls ##############################

-- A black color background is lonesome, so let's add a image to the background
background = display.newImageRect(displayGroup, "bg_space.png", width, height)
background.x = width/2
background.y = height/2

-- Let's create an associative array of walls
walls = {}
walls[1] = display.newLine(displayGroup, 0, 0, width, 0)
walls[1].tag = "topWall"

walls[2] = display.newLine(displayGroup, 0, 0, 0, height)
walls[2].tag = "leftWall"

walls[3] = display.newLine(displayGroup, width, 0, width, height)
walls[3].tag = "rightWall"

walls[4] = display.newLine(displayGroup, 0, height, width, height)
walls[4].tag = "bottomWall"

-- for i = initial value, end value(is included), How many i are added each time do ~ end
-- `#` is the number of elements
for i = 1, #walls, 1 do
    -- Change the wall thickness
    walls[i].strokeWidth = 50
    -- `physics.addBody(what you are registering, type, option)` Register to the  physics system
    physics.addBody(walls[i], "static", {density = 0.0, friction = 0.0, bounce = 1.0})
end

-- ############################## Create walls ##############################



```
Your successful if the display shows like the following image.

![](./image/execBreakoutSample3.png)
