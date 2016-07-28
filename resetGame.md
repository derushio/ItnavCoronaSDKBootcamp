# 11. ゲームをリセット

```
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
