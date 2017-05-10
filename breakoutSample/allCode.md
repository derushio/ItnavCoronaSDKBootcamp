# Breakout code as a whole

```lua
-----------------------------------------------------------------------------------------
--
-- Let's make Breakout game
-- main.lua
--
-----------------------------------------------------------------------------------------



-- ############################## What is a variable? ##############################

-- `width` contains the horizontal width (1080) of the screen
width = display.contentWidth
-- `height` contains the height(1920) of the screen
height = display.contentHeight

-- Drawing group
displayGroup = display.newGroup()

-- ############################## What is a variable? ##############################



-- ############################## What is a physics? ##############################

-- Load the function for physics and put it in the `physics` .
physics = require("physics")
-- Activate physics
physics.start(true)
physics.setGravity(0, 0)

-- ############################## What is a physics? ##############################



-- ############################## Let's make walls ##############################

-- Black back is lonesome, so let's add a background
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

-- for i = First value, Last value(Include), How many i will be added do ~ end
-- `#` is the number of elements
for i = 1, #walls, 1 do
    -- Change wall thickness
    walls[i].strokeWidth = 50
    -- `physics.addBody(bodys to be Registered, types, option)` Register for physical calculation
    physics.addBody(walls[i], "static", {density = 0.0, friction = 0.0, bounce = 1.0})
end

-- ############################## Let's make walls ##############################



-- ############################## Let's move the ball ##############################

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

-- ############################## Let's move the ball ##############################



-- ############################## Let's place blocks ##############################

maxNumBlocks = 0
numBlocks = 0

blocks = {}

function deleteBlock(index)
    -- Ignore when there is no block
    if (blocks[index] == nil) then
        -- return is an instruction to terminate the function here
        return
    end

    -- removeSelf() is a function to delete myself from the screen
    blocks[index]:removeSelf()
    -- Since it is not displayed anymore, assign nil which means nothing
    blocks[index] = nil
    -- I deleted one block, so let's set `numBlocks` to `-1` .
    numBlocks = numBlocks - 1
end

function deleteAllBlocks()
    -- Delete all blocks using for statement
    for i = 0, maxNumBlocks, 1 do
        deleteBlock(i)
    end

    -- Initialize all variables managing the block
    maxNumBlocks = 0
    numBlocks = 0
    blocks = {}
end

function deployBlocks()
    -- Delete all blocks before placing blocks
    deleteAllBlocks()

    -- Place blocks
    for y = 0, 1, 1 do
        for x = 0, 4, 1 do
            -- What number of element
            local index = x + (y * 5)
            blocks[index] = display.newImageRect(displayGroup,
                "block.png", width * 1/8, 100)
            -- (width * 1/6) => Divide the screen into six , Since the two are both ends, four can actually be used
            -- (x + 1) => What number out of the four you divided . 0 is the edge of the screen , +1 and ignore it
            blocks[index].x = (x + 1) * (width * 1/6)
            -- It will be y=0 => 400, y=1 => 600 
            blocks[index].y = 400 + (200 * y)
            blocks[index].tag = "block"
            -- Include the generated order for easy identification later
            blocks[index].index = index
            physics.addBody(blocks[index], "static", 
                {density = 0.0, friction = 0.0, bounce = 1.0})

            -- Add current block number
            numBlocks = numBlocks + 1
        end
    end

    -- Save the number of generated blocks
    maxNumBlocks = numBlocks
end

deployBlocks()

-- ############################## Let's place blocks ##############################



-- ############################## Let's arrange a racket ##############################

racket = display.newRect(displayGroup, width/2, 1700, 200, 20)
racket.tag = "racket"
racket:setFillColor(1.0, 1.0, 0.0)
physics.addBody(racket, "static", {density = 0.0, friction = 0.0, bounce = 1.0})

-- ############################## Let's arrange a racket ##############################



-- ############################## Let's move the racket ##############################

function moveRacket(xPosition)
    racket.x = xPosition
end

function displayTouchListener(event)
   moveRacket(event.x) 
end

-- Set touch event of whole screen
Runtime:addEventListener("touch", displayTouchListener)

-- ############################## Let's move the racket ##############################



-- ############################## Let's add game judgment ##############################

completeText = nil

function completeGame()
    physics.pause()
    completeText = display.newText(displayGroup, "Complete", width/2, height/2, native.systemFont, 100)
    completeText:setTextColor(1.0, 1.0, 1.0)

    Runtime:addEventListener("tap", resetGame)
end

function failGame()
    physics.pause()
    completeText = display.newText(displayGroup, "Fail", width/2, height/2, native.systemFont, 100)
    completeText:setTextColor(1.0, 1.0, 1.0)

    Runtime:addEventListener("tap", resetGame)
end

-- ############################## Let's add game judgment ##############################



-- ############################## Let's make game logic ##############################

function ballStabilization()
    -- Acquire the speed and fix the speed of x, y to 500
    local vx, vy = ball:getLinearVelocity()
        
    if (0 < vx) then
        vx = 500
    else
        vx = -500
    end

    if (0 < vy) then
        vy = 500
    else
        vy = -500
    end
    
    -- Stabilize the speed
    ball:setLinearVelocity(vx, vy)
    -- To rotate
    ball:applyTorque(90)
end

function ballCollision(event)
    if (event.phase == "began") then
        print("collision: "..event.other.tag)
    elseif (event.phase == "ended") then
        ballStabilization()

        -- Delete block when hitting block
        if (event.other.tag == "block") then
            local hitBlock = event.other
            deleteBlock(hitBlock.index)
            -- Clear judgment when there are no more blocks
            if (numBlocks == 0) then
                completeGame()
            end
        elseif (event.other.tag == "bottomWall") then
            failGame()
        end
    end
end

-- et crash event to ball
ball:addEventListener("collision", ballCollision)

-- ############################## Let's make game logic ##############################



-- ############################## Reset the game ##############################

function resetGame()
    Runtime:removeEventListener("tap", resetGame)

    completeText:removeSelf()
    completeText = nil

    physics.start(true)

    deployBlocks()
    resetBallPos()
    gameStart()
end

-- ############################## Reset the game ##############################
```