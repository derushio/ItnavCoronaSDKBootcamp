# 6. Let's place a block

## Reviewing variables
To control the number of blocks
The variable ' maxnumBlocks ' to manage how many blocks were initially placed
Now let's define a variable ' numBlocks ' to manage how many blocks there are.  
Because I do not place one at the beginning, let's put ' 0 '.
If you use a lot of blocks, You should manage them in an array.
Let's declare a table.

```lua
maxNumBlocks = 0
numBlocks = 0

blocks = {}
```

---

## Let's place a block
First, let's declare a function ' deployBlocks ' to place the blocks.  
Also, since we want to place the blocks at there initial position, write `deploy Blocks()` to be executed at timing of load.


```lua
function deployBlocks()

    -- ブロックを配置
        for x = 0, 4, 1 do
            -- 何番目の要素か
            local index = x 
            blocks[index] = display.newImageRect(displayGroup,
                "block.png", width * 1/8, 100)
            -- (width * 1/6) => 画面を6つに分ける、2つは両端なので、実際に使えるのは4つ
            -- (x + 1) => 分けた4つのうちの何番目か、0は端っこなので+1して無視する
            blocks[index].x = (x + 1) * (width * 1/6)
            -- y=0 => 400, y=1 => 600 となる
            blocks[index].y = 300
            blocks[index].tag = "block"
            -- 後で識別しやすいように生成した順番を入れておく
            blocks[index].index = index
            physics.addBody(blocks[index], "static", 
                {density = 0.0, friction = 0.0, bounce = 1.0})

            -- 現在のブロック数を追加
            numBlocks = numBlocks + 1
        end

    -- 生成したブロック数を保存
    maxNumBlocks = numBlocks
end

deployBlocks()
```

---

## Let's create a function to delete a block
' deleteBlock ', the function to remove the block from ' Index (number of array),
Declares a function ' deleteAllBlocks ' that removes all the blocks that are placed.
You must write `deleteAllBlocks` above of `deployBlocks`, it will avoid an error.

```lua
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

--　必ずdeployBlocks()の前に書いてください
function deployBlocks()



```
---

## Let's add a function to remove a block
Now we are ready to use deleteBlocks(), deployBlocks() each function.
Next, execute the function  `deleteAllBlocks` at the beginning of `deployBlocks` to remove all blocks before placing the block.

```lua

function deployBlocks()
-- ここに追加
    deleteAllBlocks()

-- ブロック配置
```

---

## Let's deploy blocks in two row.
**ブロックを配置しよう**の時点では、You have placed only one column of blocks.
But, it will be possible to clear the game as soon as it is.
Let's try to change block columns  from 1 to 2.

``` lua

function deployBlocks()
    -- ブロックを配置する前に全てのブロックを削除
    deleteAllBlocks()

    -- 下の１文を追加
    for y = 0, 1, 1 do
        for x = 0, 4, 1 do
            -- 下の1文は以下のように書き換え
            local index = x + (y * 5)
            blocks[index] = display.newImageRect(displayGroup,
                "block.png", width * 1/8, 100)
            
            blocks[index].x = (x + 1) * (width * 1/6)
            -- 下の1文は以下のように書き換え
            blocks[index].y = 400 + (200 * y)
            blocks[index].tag = "block"
            --　以下は "ブロックを配置しよう" と同じ
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


```


---


## All code in this chapter
このセクションで書いたコードの全文は以下になります。

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

```

画面は以下のようになっていれば成功です。

![](./image/execBreakoutSample5.png)
