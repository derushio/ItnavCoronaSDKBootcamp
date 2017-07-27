# 5. ボールを動かそう

## ボールを表示しよう

壁と同じようにボールも表示させましょう。  
以下のコードで表示することができます。

```lua
ball = display.newImageRect(displayGroup, "star.png", 50, 50)
ball.tag = "ball"
```

---

## 物理エンジンにボールを追加しよう

表示できたらボールを物理エンジンに追加しましょう。  
以下のコードで物理エンジンに追加されます。  
ボールは自由に動きまわるオブジェクトなので、 `"dynamic"` を指定しましょう。

```lua
physics.addBody(ball, "dynamic", {density = 0.0, friction = 0.0, bounce = 1.0})
```

---

## ボールの位置を初期化する関数を作ろう

物理エンジンに追加できたら、ボールの位置を初期位置に戻す関数 `resetBallPos` を宣言しましょう。  
`関数` とは、ひとまとまりのプログラムを名前をつけて保存できるシステムです。これが変数として保存されている場合もあります。  
以下のコードで `resetBallPos` 関数を宣言できます。使う際は `resetBallPos()` で使用することができます。

```lua
function resetBallPos()
    ball.x = width/2
    ball.y = 1200
end
```

---

## ボールを初期化してゲームを開始する関数を作ろう

ボールを初期位置に戻し、ボールを動かし始める関数 `gameStart` を宣言しましょう。  
また、ソースコードが読まれたタイミングでゲームを起動しておきたいため、 `gameStart()` を書いておきましょう。  
以下のコードで `gameStart()` をこのソースコードを読まれたタイミングで実行できます。

```lua
function gameStart()
    resetBallPos()
    ball:setLinearVelocity(0, 500)
end

gameStart()
```

参考
CoronaSDK Reference \[setLinearVelocity\]

[https://docs.coronalabs.com/api/type/Body/setLinearVelocity](https://docs.coronalabs.com/api/type/Body/setLinearVelocity.html)

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
```

画面は以下のようになっていれば成功です。

![](./image/execBreakoutSample4.png)
