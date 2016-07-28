# 11. ゲームをリセット

## ゲームをリセットする関数を追加する
ゲームをリセットするための関数 `resetGame` を追加します。    
内容は、 `resetGame` に設定されているイベントリスナを解除し、結果を通知しているテキストを削除し、物理演算を再開し、ブロック、ボールを初期配置にもどして、ゲームをスタートします。  
これを追加しただけでは、ゲームをリトライすることはできません。

```lua
function resetGame()
    Runtime:removeEventListener("tap", resetGame)

    completeText:removeSelf()
    completeText = nil

    physics.start(true)

    deployBlocks()
    resetBallPos()
    gameStart()
end
```

- - -

## ゲームのリセット関数を有効にする
以前[9. ゲーム判定を追加しよう](./checkGame.md)で追加したコードのうち、コメントアウトされていた `Runtime:addEventListener("tap", resetGame)` を有効化することで、ゲームのリトライを有効にすることができる。

```lua
function completeGame()
    physics.pause()
    completeText = display.newText(displayGroup, "Complete", width/2, height/2, native.systemFont, 100)
    completeText:setTextColor(1.0, 1.0, 1.0)

    Runtime:addEventListener("tap", resetGame)
end

function failGame()
    physics.pause()
    completeText = display.newText(displayGroup, "Fail", width/2, height/2, native.systemFont, 100)
    completeText:setTextColor(1.0, 1.0, 1.0)

    Runtime:addEventListener("tap", resetGame)
end
```

- - -

## セクション中の全文
このセクションで書いたコードの全文は以下になります。

** この変更は[9. ゲーム判定を追加しよう](./checkGame.md)の部分の上書きです **

```lua
function completeGame()
    physics.pause()
    completeText = display.newText(displayGroup, "Complete", width/2, height/2, native.systemFont, 100)
    completeText:setTextColor(1.0, 1.0, 1.0)

    Runtime:addEventListener("tap", resetGame)
end

function failGame()
    physics.pause()
    completeText = display.newText(displayGroup, "Fail", width/2, height/2, native.systemFont, 100)
    completeText:setTextColor(1.0, 1.0, 1.0)

    Runtime:addEventListener("tap", resetGame)
end
```

** この変更は新規作成部分です **

```lua
function resetGame()
    Runtime:removeEventListener("tap", resetGame)

    completeText:removeSelf()
    completeText = nil

    physics.start(true)

    deployBlocks()
    resetBallPos()
    gameStart()
end
```