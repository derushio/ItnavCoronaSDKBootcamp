# イベント系Sample
## Touchイベントの使い方例

```lua
object = display.newImage("image.png", x, y)

function onObjectTouch(event)
    if(event.phase == "began") then
        --画面を指でタッチした時の処理
    elseif(event.phase == "moved") then
        --画面を指でドラッグした時の処理
    elseif(event.phase == "ended") then
        --画面にタッチしていた指を離した時の処理
end

object:addEventListener("touch", onObjectTouch)
```

まず `local object = display.newImage("画像名", x座標, y座業)` というコードで `object` という変数名の画像を表示します。  
その画像にタッチイベントをつけるために `onObjectTouch` という名前のfunctionを作成します。  
`object:addEventListener("touch", function名)` で `object` をタッチした時にこのfunctionが呼び出されます。  
`if(event.phase == "began") then`でタッチし始めた時にこの中の処理が実行されます。  
`elseif(event.phase == "moved") then`でタッチし続けた時にこの中の処理（ドラッグ）が実行されます。  
`elseif(event.phase == "ended") then`でタッチし終わった時にこの中の処理が実行されます。

- - -

## Tapイベントの使い方

```lua
object = display.newImage("image.png", x, y)

function onObjectTap(event)
    --画面をタップした時の処理
end

object:addEventListener("tap", onObjectTap)
```

まず `local object = display.newImage("image.png", x座標, y座標)` というコードで `object` という変数名の画像を表示します。  
その画像にタップイベントをつけるために `onObjectTap` という名前のfunctionを作成します。  
`object:addEventListener("tap", function名)` で `object` をタップした時にこのfunctionが呼び出され、中の処理が実行されます。  

- - -

## Timerイベントの使い方

```lua
count = 10
time = display.newText(count, x, y, nil, 20)

function timerEvent (event)
    --１秒ごとに呼び出される
    count = count - 1
    time.text = count

    if (count == 0) then
        timer.pause(timer1)
    end
end

timer1 = timer.performWithDelay(1000, timerEvent, 0)
```

まず `count = 10` でcountという変数に10を入れます。  
そのあと `time = display.newText(count, x座標, y座標, nil, テキストサイズ)` で `count` に入れた数字を画面内に表示させます。  
その数字を変更するために `timerEvent` という名前のfunctionを作成します。  
`count = count - 1` でcount内の数字を `-1` ずつ変更します。  
次に `time.text = count` で画面に表示されている数字を `-1` ずつ変更したものに書き換えます。  
サンプルとして、もしカウントが `0` になった場合タイマーを止めるという処理を書きます。    

```lua
if (count == 0) then  
　　timer.pause(timer1)  
end
```

あとは `timer1 = timer.performWithDelay(1000, timerEvent, 0（繰り返す回数）)` で  
`1000ミリ秒（1秒）` ごとにtimerEventをずっと繰り返すという処理を書いて簡単なタイマーを作成します。  
繰り返す回数を `0` や `-1` にするとアプリケーションが起動中はずっと繰り返します。  
