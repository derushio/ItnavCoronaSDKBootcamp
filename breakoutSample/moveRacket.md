# 8. ラケットを動かそう

```lua
function racketMove(event)
    racket.x = event.x
end

function displayTouchListener(event)
   racketMove(event) 
end

-- 画面全体のタッチイベントを設定
Runtime:addEventListener("touch", displayTouchListener)
```