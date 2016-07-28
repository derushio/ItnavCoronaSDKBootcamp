# API Sample

## 円を表示する

```
local circle = display.newCircle(100, 200, 20)
circle:setFillColor(1, 1, 0, 0.5)
```

上のコードを入力すると半径２０の円がx＝100、y＝200のところに表示されます。円の色を2行目のコードで設定します。

## 長方形を表示する
```
local rectangle = display.newRect(100, 200, 40, 30)
```

上のコードを入力するとx＝100、y＝200に横40、縦30の長方形が表示されます。

## テキストを表示する
```
local text = display.newText("テキストです", 100, 200, native.systemFont, 16)
```

上のコードを入力すると「テキストです」がx＝100、y＝200にサイズ１６で表示されます。

## 画像を表示する
```
local rect = display.newImageRect("dice.png", 100, 200)
```

上のコードを入力するとサイコロの絵（"dice.png"）がx＝100、y＝200に表示されます

## 線を表示する
```
local line = display.newLine(10, 20, 30, 40)
```

上のコードを入力すると線がx＝10、y＝20からx＝30、y＝40に描かれます。

## グループ作成
```
local group = display.newGroup()
group:insert(line)
```

上のコードを入力すると先ほど作った線が新しいグループに追加されます。

## 端末の幅を取得
```
display.contentWidth
```

wが端末の幅の長さです。

## 端末の高さを取得
```
display.contentHeight
```

hが端末の高さです。

## 絶対値を表示
```
local b = math.abs(-15)
```

bは15になります。

## ランダムに数字を出す
```
math.random(10)
```
ランダムに１から１０までの整数を一つ表示します。

## Sin 
```
math.sin(x)
```

−１から１までの数字をx（ラジアン）を元に出します。

## Cos
```
math.cos(x)
```

−１から１までの数字をx（ラジアン）を元に出します。


## Tan
```
math.tan(x)
```

tanを出します。

## pi
```
math.pi
```
πを出します。

## 物理エンジンにオブジェクトを追加する
```
physics.addBody(circle, "static", {density = 1, friction = 0.3, bounce = 0.4})
```

円をディフォルトの"dynamic"から"static"に変え、{}の中にオプショナルな物理的条件を入れます。

## 物理エンジンを開始
```
local physics = require("physics")
physics.start()
```

物理エンジンを開始します。

## 重力を設定する
```
physics.setGravity(x、y)
```

ディフォルトの（０,⒐８）から重力を変える時に使います。

## 物理エンジンを一時停止する
```
physics.pause()
```

## 物理エンジンに入れたオブジェクトを取り除く
```
physics.removeBody(object)
```

## オブジェクトの速さを設定する
```
object:setLinearVelocity(x、y)
```







