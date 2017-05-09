# 2. What is variable?

## 'variable' is ...

Programming language has a system called 'variable'.<br />
'variable' can store numbers and objects and more.<br />
<br />
Lua language for example,<br />
`number = 10`<br />
This means in `number` 10 is stored.<br />
<br />
lua language has static 'variable' for environment.<br />
They are `display.contentWidth` and `display.contentHeight` and more.<br />
<br />
But, they are too long to spell and you maybe use them many times.<br />
Too long spell is a hassle.<br />
You can use short spell variable for environment variable.<br />
<br />
If you create your own variable and for example you name it width, You can write like `width = display.contentWidth`.<br />
Write `=` in the center, variable on the left, variable or objects on the right.<br />
Try writing this code, `content width` will be stored in `width` and `content height` will be stored in `height`.<br />

```lua
-- `width` は画面の横幅(1080)が入っている
width = display.contentWidth
-- `height` は画面の縦幅(1920)が入っている
height = display.contentHeight
```

After you write your code, it must be saved. Use shortcut command for Windows-> `ctrl + s`, for Mac -> `Command + s`.<br />
If errors weren't found , it was a success.<br />

---

## Create display group

Create a display group to draw a screen view for CoronaSDK, and store it in variable `displayGroup`.<br />
Try this code.<br />

```lua
-- 描画グループ
displayGroup = display.newGroup()
```

from<br />
CoronaSDK Reference [displayGroup]<br />

[https://docs.coronalabs.com/api/library/display/newGroup](https://docs.coronalabs.com/api/library/display/newGroup.html)

---

## All code in this chapter

All code in this chapter

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




```

If your display shows like the following image, it is a success.<br />

![](./image/execBreakoutSample1.png)

