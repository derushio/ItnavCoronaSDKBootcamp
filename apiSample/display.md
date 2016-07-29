# 画面表示系Sample

## 円を表示する

```lua
local circle = display.newCircle(100, 200, 20)
circle:setFillColor(1, 1, 0, 0.5)
```

上のコードを入力すると半径２０の円がx＝100、y＝200のところに表示されます。円の色を2行目のコードで設定します。

- - -

## 長方形を表示する

```lua
local rectangle = display.newRect(100, 200, 40, 30)
```

上のコードを入力するとx＝100、y＝200に横40、縦30の長方形が表示されます。

- - -

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

- - -

## 画像を表示する

```lua
local rect = display.newImageRect("dice.png", 100, 200)
```

上のコードを入力するとサイコロの絵（"dice.png"）がx＝100、y＝200に表示されます

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