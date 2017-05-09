# 3. Physics is ...

## Physics is ...
CoronaSDK has physics system. (Physics system can emulate of movement bouncing ball and more.)
You can use physics from this code.

```lua
-- 物理演算をするための機能を読み込んで `physics` に入れておく
physics = require("physics")
-- 物理演算を起動する
physics.start(true)
physics.setGravity(0, 0)
```

now, it is not working. but, it will work hard since next chapter.

from
CoronaSDK Reference [physics]

[https://docs.coronalabs.com/api/library/physics/index](https://docs.coronalabs.com/api/library/physics/index.html)

---

## All code in this chapter
All code in this chapter

```lua
-----------------------------------------------------------------------------------------
--
-- ピンボールゲームを作ってみよう
-- main.lua
--
-----------------------------------------------------------------------------------------



-- ############################## 変数とは？ ##############################

-- `width` は画面の横幅(1080)が入っている
width = display.contentWidth
-- `height` は画面の縦幅(1920)が入っている
height = display.contentHeight

-- 描画グループ
displayGroup = display.newGroup()

-- ############################## 変数とは？ ##############################



-- ############################## 物理演算とは？ ##############################

-- 物理演算をするための機能を読み込んで `physics` に入れておく
physics = require("physics")
-- 物理演算を起動する
physics.start(true)
physics.setGravity(0, 0)

-- ############################## 物理演算とは？ ##############################


```
display is like this pic.<br />
still same view of prev chapter.

![](./image/execBreakoutSample2.png)
