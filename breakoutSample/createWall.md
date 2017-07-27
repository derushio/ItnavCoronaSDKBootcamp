# 4. 壁を作ろう

## 背景を表示しよう
背景が黒では寂しいので、以下のコードで背景を描画しましょう。

```lua
-- 背景黒では寂しいので、背景を追加しましょう
background = display.newImageRect(displayGroup, "bg_space.png", width, height)
background.x = width/2
background.y = height/2
```

参考：CoronaSDK Reference [newImageRect]

[https://docs.coronalabs.com/api/library/display/newImageRect
](https://docs.coronalabs.com/api/library/display/newImageRect.html)

---

## 壁を表示しよう
ボールが動いた時に跳ね返るように壁を作っておきましょう。  
壁は四角形を四隅に配置して作ろうと思うので、 `display.newLine(LeftTopのX座標, LeftTopのY座標, RightBottomのX座標, RightBottomのY座標)` という機能を使って壁を作りたいと思います。  
しかし、4つ作るからといって  
`walls1 = display.newLine(displayGroup, 0, 0, width, 0)`  
`walls2 = display.newLine(displayGroup, 0, 0, 0, height)`  
...  
とするのはあまり格好良くありません。  
そこで、テーブルを使ってみましょう。  
テーブルは `walls = {}` で宣言でき、 `walls[0]`, `walls[1]` のような形でアクセスできます。  
また、変数の内容を識別しやすいように `tag` にどこの壁なのかを入れておきましょう。  

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




参考
CoronaSDK Reference [newLine]

[https://docs.coronalabs.com/api/library/display/newLine](https://docs.coronalabs.com/api/library/display/newLine.html)

---

## for文で壁を一括で設定してみよう
配列にするとfor文で一括処理をすることができます。
for文とは、 `for i = 最初の値, 最後の値(含む), 幾つづつiをプラスするか do ~ end` の構文で最初の値から最後の値になるまで `do ~ end` の内容を実行します。
for文で壁の厚さを変更、物理演算に登録を一括でやってみましょう。  
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
