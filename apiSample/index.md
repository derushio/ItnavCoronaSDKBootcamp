# API Sample

## 円を表示する

```lua
local circle = display.newCircle(100, 200, 20)
circle:setFillColor(1, 1, 0, 0.5)
```

上のコードを入力すると半径２０の円がx＝100、y＝200のところに表示されます。円の色を2行目のコードで設定します。

## 長方形を表示する

```lua
local rectangle = display.newRect(100, 200, 40, 30)
```

上のコードを入力するとx＝100、y＝200に横40、縦30の長方形が表示されます。

## テキストを表示する

```lua
local textT = display.newText("テキストです", 100, 200, native.systemFont, 16)
```

上のコードを入力すると「テキストです」がx＝100、y＝200にサイズ１６で表示されます。

## テキストをアップロードする

```lua
textT.text = "テキスト書き直しました。"
```

テキストを元の「テキストです」から「テキスト書き直しました。」に書き換えます。

## 画像を表示する

```lua
local rect = display.newImageRect("dice.png", 100, 200)
```

上のコードを入力するとサイコロの絵（"dice.png"）がx＝100、y＝200に表示されます

## 線を表示する

```lua
local line = display.newLine(10, 20, 30, 40)
```

上のコードを入力すると線がx＝10、y＝20からx＝30、y＝40に描かれます。

## グループ作成

```lua
local group = display.newGroup()
group:insert(line)
```

上のコードを入力すると先ほど作った線が新しいグループに追加されます。

## 端末の幅を取得

```lua
display.contentWidth
```

wが端末の幅の長さです。

## 端末の高さを取得

```lua
display.contentHeight
```

hが端末の高さです。

## 絶対値を表示

```lua
local b = math.abs(-15)
```

bは15になります。

## ランダムに数字を出す

```lua
math.random(10)
```
ランダムに１から１０までの整数を一つ表示します。

## Sin 

```lua
math.sin(x)
```

−１から１までの数字をx（ラジアン）を元に出します。

## Cos

```lua
math.cos(x)
```

−１から１までの数字をx（ラジアン）を元に出します。

## Tan

```lua
math.tan(x)
```

tanを出します。

## pi

```lua
math.pi
```
πを出します。

## 物理エンジンにオブジェクトを追加する

```lua
physics.addBody(circle, "static", {density = 1, friction = 0.3, bounce = 0.4})
```

円をディフォルトの"dynamic"から"static"に変え、{}の中にオプショナルな物理的条件を入れます。

## 物理エンジンを開始

```lua
local physics = require("physics")
physics.start()
```

物理エンジンを開始します。

## 重力を設定する

```lua
physics.setGravity(x、y)
```

ディフォルトの（０,⒐８）から重力を変える時に使います。

## 物理エンジンを一時停止する

```lua
physics.pause()
```

## 物理エンジンに入れたオブジェクトを取り除く

```lua
physics.removeBody(object)
```

## オブジェクトの速さを設定する

```lua
object:setLinearVelocity(x、y)
```

x軸の速さとy軸の速さをかっこに入れて速さを設定します。

## オブジェクトがスクリーンに出るか

```lua
rect.isVisible = true
```

ブーリアンでコントロールします。






