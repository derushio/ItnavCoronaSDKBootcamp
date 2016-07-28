# 10. ボールの角度と速度を安定させよう

```lua
function ballStabilization()
    -- 速度を取得して、x,yの速度を500に固定する
    local vx, vy = ball:getLinearVelocity()
        
    if (0 < vx) then
        vx = 500
    else
        vx = -500
    end

    if (0 < vy) then
        vy = 500
    else
        vy = -500
    end
    
    -- 速度を安定させる
    ball:setLinearVelocity(vx, vy)
    -- 回転させる
    ball:applyTorque(90)
end

function ballCollision(event)
    if (event.phase == "began") then
        print("collision: "..event.other.tag)
    elseif (event.phase == "ended") then
        ballStabilization()

        -- ブロックに当たった時はブロックを削除
        if (event.other.tag == "block") then
            local hitBlock = event.other
            deleteBlock(hitBlock.index)
            -- ブロックがなくなった場合はクリア判定
            if (numBlocks == 0) then
                completeGame()
            end
        elseif (event.other.tag == "bottomWall") then
            failGame()
        end
    end
end

-- 衝突イベントをボールに設定
ball:addEventListener("collision", ballCollision)
```