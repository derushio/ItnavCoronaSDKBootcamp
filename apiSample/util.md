# 便利系Sample

## 端末の幅を取得

```lua
display.contentWidth
```

display.contentWidthが端末の幅の長さです。

参考
CoronaSDK Reference　[contentWidth]

[https://docs.coronalabs.com/api/library/display/contentWidth](https://docs.coronalabs.com/api/library/display/contentWidth.html)

---

## 端末の高さを取得

```lua
display.contentHeight
```

display.contentHeightが端末の高さです。

CoronaSDK Reference[contentHeight]

[https://docs.coronalabs.com/api/library/display/contentHeight](https://docs.coronalabs.com/api/library/display/contentHeight.html)

---

## テキストボックスを生成する

``` lua

defaultBox.newTextBox( centerX, centerY, width, height )

-- テキストボックスを編集可能にする
defaultBox.isEditable = true

```

centerXはx座標の位置を、centerYはY座標の位置を指定でき、
widthは横幅を、heightは高さを指定できます。
isEditableは"false"を入力すると編集できなくなります。


参考
CoronaSDK Reference[newTextBox]
[https://docs.coronalabs.com/api/library/native/newTextBox](https://docs.coronalabs.com/api/library/native/newTextBox.html)

---

## テキストボックスに入力した内容を表示する

下のボタンを押すと、テキストボックスに入力した内容がテキストボックスの上に表示されるプログラムです。


``` lua

-----------------------------------------------------------------------------------------
--テキストボックスを作ってみよう

-- main.lua
--
-----------------------------------------------------------------------------------------

--　画面の横幅(1080)を取得し、変数”width”に入れる
width = display.contentWidth

--　画面の縦幅(1920)を取得し、変数"height"に入れる
height = display.contentHeight

-- 描画グループを作る
displayGroup = display.newGroup()


-- テキストボックスに表示されている文字を入れる変数を宣言
editText = ""

-- テキストを表示する関数
local function textView()
local text = display.newText(editText, width/2, height/7, native.systemFont, 60)
text:setFillColor(0, 0.5, 1)

end

-- テキストボックスに入力した文字を表示するボタンを作る
local widget = require( "widget" )

local function handleButtonEvent( event )

    if( "ended" == event.phase ) then
        textView()

    end
end

-- ボタンの設定
local textButton = widget.newButton(
    {
        left = 450,
        top = 1620,
        fontSize = 50,
        id = "button1",
        label = "Default",
        onEvent = handleButtonEvent

    }
) 


-- テキストボックスevent時の設定関数を作る
function textListener(event)

    -- 編集を始める時
    if( event.phase == "began" ) then

    -- 終わったもしくは投稿したとき
    elseif( event.phase == "ended" or event.phase == "submitted" ) then
        print( event.target.text )
        editText = event.target.text
        print(editText)

    -- 編集中
    elseif( event.phase == "editing" ) then
        print( event.newCharacters )
        --print( event.startPosition )
        print( event.text )

    end
end
-- テキストボックスを生成( x, y, 横の大きさ, 縦の大きさ )
textBox = native.newTextBox( 540, 960, width, height/2 )
-- 編集できるように設定

textBox.isEditable = true
textBox:addEventListener( "userInput", textListener )


```




## 音を再生する

[外部リンク](http://kwiksher.com/bootcamp/corona1/playing_audio.html)

---

## 画面遷移
[外部リンク](http://kwiksher.com/bootcamp/corona2/composer_gui.html)