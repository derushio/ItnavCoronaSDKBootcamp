# 画面表示系Sample

## 円を表示する

```lua
display.newCircle(x座標, y座標, 半径)
```

```lua
local circle = display.newCircle(100, 200, 20)
circle:setFillColor(1, 1, 0, 0.5)
```

上のコードを入力すると `半径20` の円が `(x＝100,y＝200)` のところに表示されます。  
円の色を2行目のコードで設定します。

- - -

## 長方形を表示する

```lua
display.newRect(長方形の左上のx座標, 長方形の左上のy座標, 幅, 高さ)
```

```lua
local rectangle = display.newRect(100, 200, 40, 30)
```

上のコードを入力すると `(x＝100, y＝200)` に `幅40` 、 `高さ30` の長方形が表示されます。

- - -

## テキストを表示する

```lua
display.newText(表示するテキスト, x座標, y座標, フォント名, 文字の大きさ)
```

```lua
local textT = display.newText("テキストです", 100, 200, native.systemFont, 16)
```

上のコードを入力すると `「テキストです」` が `(x＝100, y＝200)` に `文字の大きさ16` で表示されます。

## テキストを変更する

```lua
textT.text = "テキスト書き直しました。"
```

`テキストの変数名.text` で今表示しているテキストにアクセスできます。取得や設定もこの変数からできます。

- - -

## 画像を表示する

```lua
display.newImageRect(画像の名前, 幅, 高さ)
```

```lua
local rect = display.newImageRect("dice.png", 100, 200)
```

上のコードを入力すると `サイコロの絵("dice.png")` が `(x＝100, y＝200)` に表示されます。

- - -

## 線を表示する

```lua
local line = display.newLine(10, 20, 30, 40)
```

上のコードを入力すると線がx＝10、y＝20からx＝30、y＝40に描かれます。

- - -

## グループ作成

```lua
local group = display.newGroup()
group:insert(line)
```

上のコードを入力すると先ほど作った線が新しいグループに追加されます。  
グループとは、画面に表示されているオブジェクトをまとめて管理するシステムで、まとめて画面から表示されているオブジェクトを削除したりするときに便利です。