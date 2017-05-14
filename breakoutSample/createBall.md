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
-- ピンボールゲームを作ってみよう
-- main.lua
--
-----------------------------------------------------------------------------------------



-- ############################## 変数とは？ ##############################

-- `width` は画面の横幅(1080)が入っている
width = display.contentWidth
-- `height` は画面の縦幅(1920)が入っている
height = display.contentHeight

-- 描画グループ
displayGroup = display.newGroup()

-- ############################## 変数とは？ ##############################



-- ############################## 物理演算とは？ ##############################

-- 物理演算をするための機能を読み込んで `physics` に入れておく
physics = require("physics")
-- 物理演算を起動する
physics.start(true)
physics.setGravity(0, 0)

-- ############################## 物理演算とは？ ##############################



-- ############################## 壁を作ろう ##############################

-- 背景黒では寂しいので、背景を追加しましょう
background = display.newImageRect(displayGroup, "bg_space.png", width, height)
background.x = width/2
background.y = height/2

-- 壁の連想配列を作ろう
walls = {}
walls[1] = display.newLine(displayGroup, 0, 0, width, 0)
walls[1].tag = "topWall"

walls[2] = display.newLine(displayGroup, 0, 0, 0, height)
walls[2].tag = "leftWall"

walls[3] = display.newLine(displayGroup, width, 0, width, height)
walls[3].tag = "rightWall"

walls[4] = display.newLine(displayGroup, 0, height, width, height)
walls[4].tag = "bottomWall"

-- for i = 最初の値, 最後の値(含む), 幾つづつiをプラスするか do ~ end
-- `#` は要素数
for i = 1, #walls, 1 do
    -- 壁の厚さを変更
    walls[i].strokeWidth = 50
    -- `physics.addBody(登録する物, 種類, オプション)` 物理演算に登録
    physics.addBody(walls[i], "static", {density = 0.0, friction = 0.0, bounce = 1.0})
end

-- ############################## 壁を作ろう ##############################



-- ############################## ボールを動かそう ##############################

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

-- ############################## ボールを動かそう ##############################


```

Your successful if the display shows like the following image.

![](./image/execBreakoutSample4.png)

