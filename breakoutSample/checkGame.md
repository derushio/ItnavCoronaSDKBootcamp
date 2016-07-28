# 9. ゲーム判定を追加しよう

```lua
completeText = nil

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
