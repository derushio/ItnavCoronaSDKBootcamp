# 8. ラケットを動かそう

## ラケットを動かす関数を作ろう
ラケットを動かすための関数 `moveRacket` を作りましょう。  
ラケットはy座標を自由に動かせるとブロック崩しとして成り立たなくなるので、x軸だけ移動するような関数を作りましょう。  
この程度の処理であれば関数化する必要はあまり無いですが、ラケットの移動については拡張する場合があるので念の為に関数化しておきましょう。

```lua
function moveRacket(xPosition)
    racket.x = xPosition
end
```

---

## タッチイベントを設定
今回はラケットをタッチイベントで動かしましょう。  
タッチイベントを受け取る関数 `displayTouchListener` を宣言しましょう。  
この関数を `Runtime:addEventListener("touch", displayTouchListener)` で登録することによって、 `Runtime` は画面全体なので、画面全体のどこかをタッチした瞬間に `displayTouchListener` が呼ばれるようになります。  
また、 `"touch"` イベントの場合は `タッチを開始した瞬間` `タッチした指を動かした瞬間` `タッチを終えた瞬間` に呼び出されます。  
ですので、タッチしている間に指の座標が動くと基本的に `displayTouchListener` が呼ばれます。  
タッチした座標は `event.x, event.y` で取得することができます。

```lua
function displayTouchListener(event)
   moveRacket(event.x) 
end

-- 画面全体のタッチイベントを設定
Runtime:addEventListener("touch", displayTouchListener)
```

参考：CoronaSDK Reference[addEventListener]

[https://docs.coronalabs.com/api/type/EventDispatcher/addEventListener](https://docs.coronalabs.com/api/type/EventDispatcher/addEventListener.html)


---

## セクション中の全文
このセクションで書いたコードの全文は以下になります。

```lua
function moveRacket(xPosition)
    racket.x = xPosition
end

function displayTouchListener(event)
   moveRacket(event.x) 
end

-- 画面全体のタッチイベントを設定
Runtime:addEventListener("touch", displayTouchListener)
```

画面は以下のようになっていれば成功です。  
ラケットが動くようになります。

![](./image/execBreakoutSample7.png)
