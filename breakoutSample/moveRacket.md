# 8. Let's move the racket.

## Make a function to move the racket.
Let's make a function `moveRacket` to move the racket.  
Let's create a function that will only move on the x axis, since if the racket can move on the y axis freely it does not hold as a Breakout.
There is not much need to make it into a function if it is this level of processing, but the racket movement may be extended, so let's make it as a function just in case.

```lua
function moveRacket(xPosition)
    racket.x = xPosition
end
```

---

## Set touch event.
This time we will make the racket move with a touch event.
Declare the function `displayTouchListener` to receive the touch event.  
By registering this function with `Runtime:addEventListener("touch" displayTouchListener)` ,`Runtime` is the entire screen, so `displayTouchListener` will be called at the moment you touch somewhere on the screen. 
Also, the case of the `"touch"` event, it will be called `At the start of touch` `At the start of swipe` `At the end of touch`.
So basically during you are touching the screen, if your finger coordinate moves `displayTouchListener` will be called.
You can get the coordinate you touched by `event.x, event.y`.

```lua
function displayTouchListener(event)
   moveRacket(event.x) 
end

-- Set touch event of whole screen
Runtime:addEventListener("touch", displayTouchListener)
```

Reference
CoronaSDK Reference[addEventListener]

[https://docs.coronalabs.com/api/type/EventDispatcher/addEventListener](https://docs.coronalabs.com/api/type/EventDispatcher/addEventListener.html)


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



-- ############################## ブロックを配置してみよう ##############################

maxNumBlocks = 0
numBlocks = 0

blocks = {}

function deleteBlock(index)
    -- ブロックが存在しない場合は無視する
    if (blocks[index] == nil) then
        -- returnはここで関数を終了させる命令です
        return
    end

    -- removeSelf()は自分を画面から消す関数です
    blocks[index]:removeSelf()
    -- もう表示されていないので空を表す `nil` を入れておきましょう
    blocks[index] = nil
    -- 一つブロックを削除したので、 `numBlocks` を `-1` しておきましょう
    numBlocks = numBlocks - 1
end

function deleteAllBlocks()
    -- for文でブロックを全て削除
    for i = 0, maxNumBlocks, 1 do
        deleteBlock(i)
    end

    -- ブロックを管理している変数を全て初期化する
    maxNumBlocks = 0
    numBlocks = 0
    blocks = {}
end

function deployBlocks()
    -- ブロックを配置する前に全てのブロックを削除
    deleteAllBlocks()

    -- ブロックを配置
    for y = 0, 1, 1 do
        for x = 0, 4, 1 do
            -- 何番目の要素か
            local index = x + (y * 5)
            blocks[index] = display.newImageRect(displayGroup,
                "block.png", width * 1/8, 100)
            -- (width * 1/6) => 画面を6つに分ける、2つは両端なので、実際に使えるのは4つ
            -- (x + 1) => 分けた4つのうちの何番目か、0は端っこなので+1して無視する
            blocks[index].x = (x + 1) * (width * 1/6)
            -- y=0 => 400, y=1 => 600 となる
            blocks[index].y = 400 + (200 * y)
            blocks[index].tag = "block"
            -- 後で識別しやすいように生成した順番を入れておく
            blocks[index].index = index
            physics.addBody(blocks[index], "static", 
                {density = 0.0, friction = 0.0, bounce = 1.0})

            -- 現在のブロック数を追加
            numBlocks = numBlocks + 1
        end
    end

    -- 生成したブロック数を保存
    maxNumBlocks = numBlocks
end

deployBlocks()

-- ############################## ブロックを配置してみよう ##############################



-- ############################## ラケットを配置しよう ##############################

racket = display.newRect(displayGroup, width/2, 1700, 200, 20)
racket.tag = "racket"
racket:setFillColor(1.0, 1.0, 0.0)
physics.addBody(racket, "static", {density = 0.0, friction = 0.0, bounce = 1.0})

-- ############################## ラケットを配置しよう ##############################



-- ############################## ラケットを動かそう ##############################

function moveRacket(xPosition)
    racket.x = xPosition
end

function displayTouchListener(event)
   moveRacket(event.x) 
end

-- 画面全体のタッチイベントを設定
Runtime:addEventListener("touch", displayTouchListener)

-- ############################## ラケットを動かそう ##############################


```
It's a success if the display looks like the following image. 
The racket will move.

![](./image/execBreakoutSample7.png)
