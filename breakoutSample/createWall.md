# 4. Create walls

## Draw background image
You can draw background by this code.

```lua
-- 背景黒では寂しいので、背景を追加しましょう
background = display.newImageRect(displayGroup, "bg_space.png", width, height)
background.x = width/2
background.y = height/2
```

from：CoronaSDK Reference [newImageRect]

[https://docs.coronalabs.com/api/library/display/newImageRect
](https://docs.coronalabs.com/api/library/display/newImageRect.html)

---

## Draw walls
Create walls for moving ball keep on inside of the display.<br />
Walls should be 4 sides. it can use `display.newLine(LeftTop X position, LeftTop Y position, RightBottom X position, RightBottom Y position)`<br />
<br />
But, 4 walls create by<br />
`walls1 = display.newLine(displayGroup, 0, 0, width, 0)`<br />
`walls2 = display.newLine(displayGroup, 0, 0, 0, height)`<br />
They are bad.<br />
<br />
So, You can use table system.<br />
table is deffined `walls = {}`, you can access variable by `walls[0]`, `walls[1]`.<br />
and, variable value should be defined `tag` for you understand where block place.<br />

```lua
以下のコードを書き、壁を描画してみましょう。 
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
```

from<br />
CoronaSDK Reference [newLine]

[https://docs.coronalabs.com/api/library/display/newLine](https://docs.coronalabs.com/api/library/display/newLine.html)

---

## Draw walls draw by `for system`
If use array, You can draw walls at one time by `for system`.
`for system` is written `for i = initial value, finish value, what value plus i do ~ end`
When it is execute between `do ~ end`, i value is from init value to finish value.
Let's draw walls by `for system`.
  
`physics.addBody(登録する物, 種類, オプション)` で物理演算に登録できます。種類は"static"で移動しないオブジェクト、"dynamic"で移動するオブジェクトです。 "kinematic"は"dynamic"と同じようにオブジェクトが動きますが、重力に沿って動く"dynamic"とは違い、"kinematic"は重力とは関係なしに移動します。
以下のコードを入力してみましょう。

```lua
-- for i = 最初の値, 最後の値(含む), 幾つづつiをプラスするか do ~ end
-- `#` は要素数
for i = 1, #walls, 1 do
    -- 壁の厚さを変更
    walls[i].strokeWidth = 50
    -- `physics.addBody(登録する物, 種類, オプション)` 物理演算に登録
    physics.addBody(walls[i], "static", {density = 0.0, friction = 0.0, bounce = 1.0})
end
```

参考
CoronaSDK Reference[addBody]

[https://docs.coronalabs.com/api/library/physics/addBody](https://docs.coronalabs.com/api/library/physics/addBody.html)

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



```
画面は以下のようになっていれば成功です。

![](./image/execBreakoutSample3.png)
