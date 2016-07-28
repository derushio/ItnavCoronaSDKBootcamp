# 6. ブロックを配置してみよう

```lua
maxNumBlocks = 0
numBlocks = 0

blocks = {}

function deleteBlock(index)
    if (blocks[index] == nil) then
        return
    end

    blocks[index]:removeSelf()
    blocks[index] = nil
    numBlocks = numBlocks - 1
end

function deleteAllBlocks()
    for i = 0, maxNumBlocks, 1 do
        deleteBlock(i)
    end

    maxNumBlocks = 0
    numBlocks = 0
    blocks = {}
end

function deployBlocks()
    -- ブロックを配置する前に全てのブロックを削除
    deleteAllBlocks()

    -- ブロックを配置
    for y = 0, 1, 1 do
        for x = 0, 4, 1 do
            -- 何番目の要素か
            local index = x + (y * 5)
            blocks[index] = display.newImageRect(displayGroup, "block.jpg", width * 1/8, 100)
            blocks[index].x = (x + 1) * (width * 1/6)
            blocks[index].y = 400 + (200 * y)
            blocks[index].tag = "block"
            blocks[index].index = index
            physics.addBody(blocks[index], "static", {density = 0.0, friction = 0.0, bounce = 1.0})

            numBlocks = numBlocks + 1
        end
    end

    maxNumBlocks = numBlocks
end

deployBlocks()
```