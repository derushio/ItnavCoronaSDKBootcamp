# 5. Let's try moving the ball.

## Display the ball.

Let's display the ball as well as the wall.
You can display it by the following code.

```lua
ball = display.newImageRect(displayGroup, "star.png", 50, 50)
ball.tag = "ball"
```

---

## Add the ball to the physics engine.

Once you have displayed the ball, let's add it to the physics engine. 
The following code adds it to the physics engine.
The ball is an object that moves freely, so let's assign ' dynamic '.

```lua
physics.addBody(ball, "dynamic", {density = 0.0, friction = 0.0, bounce = 1.0})
```

---

## Make a function to initialize the ball position.

Once you have added to the physical engine, declare the function ' resetBallPos ' to restore the position of the ball to its initial position.

A ' function ' is a system that allows you to name and save programs as a bundle.
This may be stored as a variable.
You can declare the ' resetBallPos ' function with the following code. Write ' resetBallPos() ' when using.

```lua
function resetBallPos()
    ball.x = width/2
    ball.y = 1200
end
```

---

## Create a function to initialize the ball and start the game.

Declare the function ' gameStart ' to set the ball to its initial position and then start moving the ball.  
Also, because you want to start the game when the source code is read, ' gameStart() ' should be written.  
You can run ' gameStart() ' by the following code when the source code is read.

```lua
function gameStart()
    resetBallPos()
    ball:setLinearVelocity(0, 500)
end

gameStart()
```

reference
CoronaSDK Reference \[setLinearVelocity\] 
 
[https://docs.coronalabs.com/api/type/Body/setLinearVelocity](https://docs.coronalabs.com/api/type/Body/setLinearVelocity.html)

---


## All code in this chapter
All code in this chapter

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



-- ############################## phisics is ... ##############################

-- Load the function to use the physics engine and put it in `physics` .
physics = require("physics")
-- Activate physics engine
physics.start(true)
physics.setGravity(0, 0)

-- ############################## phisics is ... ##############################



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



-- ############################## Let's try moving the ball ##############################

ball = display.newImageRect(displayGroup, "star.png", 50, 50)
ball.tag = "ball"
physics.addBody(ball, "dynamic", {density = 0.0, friction = 0.0, bounce = 1.0})

function resetBallPos()
    ball.x = width/2
    ball.y = 1200
end

function gameStart()
    resetBallPos()
    ball:setLinearVelocity(0, 500)
end

gameStart()

-- ############################## Let's try moving the ball ##############################


```

Your successful if the display shows like the following image.

![](./image/execBreakoutSample4.png)

