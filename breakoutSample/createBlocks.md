# 6. ブロックを配置してみよう

## 変数のおさらい
ブロックの数を制御するために、  
ブロックをいくつ最初に配置したのか管理する変数 `maxNumBlocks`、  
今ブロックがいくつあるのか管理する変数 `numBlocks` を定義しましょう。  
最初は一つも置いていないので、 `0` を入れておきましょう。  
また、ブロックはたくさんあるので配列で管理します。テーブルを宣言しておきましょう。

```lua
maxNumBlocks = 0
numBlocks = 0

blocks = {}
```

---

## ブロックを配置しよう
まず、ブロックを配置する関数 `deployBlocks` を宣言しましょう。  
また、ゲーム開始時にブロックを初期配置しておきたいので、 `deployBlocks()` 読み込み時に実行するように書いておきましょう。


```lua
function deployBlocks()

    -- ブロックを配置
        for x = 0, 4, 1 do
            -- 何番目の要素か
            local index = x
            blocks[index] = display.newImageRect(displayGroup,
                "block.png", width * 1/8, 100)
            -- (width * 1/6) => 画面を7つに分ける、2つは両端なので、実際に使えるのは5つ
            -- (x + 1) => 分けた7つのうちの何番目か、0は端っこなので+1して無視する
            blocks[index].x = (x + 1) * (width * 1/6)
            -- y=0 => 400, y=1 => 600 となる
            blocks[index].y = 400
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

## ブロックを削除する関数を作ろう
`index(配列の何番目か)` から、ブロックを削除する関数 `deleteBlock` 、
配置されているブロックを全て削除する関数 `deleteAllBlocks` を宣言します。
先程書いた`deployBlock`のコードの上に書かなければエラーになってしまいますので、注意してください。

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
function deployBlocks() <- これを書けというわけではなく、
この関数の前に上のfunctionを書きましょうということ
```
---

## ブロックを削除する関数を追加しよう
配置と削除、それぞれの関数の準備ができたと思います。
次に、ブロックを配置する前に全てのブロックを削除する関数`deleteAllBlocks`をdeployBlocksのはじめに実行するようにしましょう。

```lua
-- この章のはじめに書いたdeployBlocks()の最初に
-- deleteAllBlocks()の1文を追加
function deployBlocks()
-- ここに追加
    deleteAllBlocks()

-- ブロック配置
```

---

## ブロックを２列にしてみよう
**ブロックを配置しよう** の時点では、ブロックを１列だけ配置しました。
しかし、1列ではすぐにゲームクリアできてしまいます。
そこで、配置するブロックを１列から２列にしてみましょう。

``` lua
-- 上で書いたdeployBlocksを以下のように変更
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

            -- (width * 1/6) => 画面を7つに分ける、2つは両端なので、実際に使えるのは5つ
            -- (x + 1) => 分けた7つのうちの何番目か、0は端っこなので+1して無視する
            blocks[index].x = (x + 1) * (width * 1/6)
            -- 下の1文は以下のように書き換え
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


```


---


## セクション中の全文
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
            -- (width * 1/6) => 画面を7つに分ける、2つは両端なので、実際に使えるのは5つ
            -- (x + 1) => 分けた7つのうちの何番目か、0は端っこなので+1して無視する
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
