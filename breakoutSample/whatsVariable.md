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
-- `width` contains the width(1080) of the display
width = display.contentWidth
-- `height` contains the height(1920) of the display
height = display.contentHeight
```

After you write your code, it must be saved. Use shortcut command for Windows-> `ctrl + s`, for Mac -> `Command + s`.<br />
If errors weren't found , it was a success.<br />

---

## Create display group

Create a display group to draw a screen view for CoronaSDK, and store it in variable `displayGroup`.<br />
Try this code.<br />

```lua
-- display group(necassary to draw the display with coronaSDK)
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
-- Let's make Breakout
-- main.lua
--
-----------------------------------------------------------------------------------------



-- ############################## What is variable？ ##############################

-- `width` contains the width(1080) of the display
width = display.contentWidth
-- `height` contains the height(1920) of the display
height = display.contentHeight

-- display group(necassary to draw the display with coronaSDK)
displayGroup = display.newGroup()

-- ############################## What is variable？ ##############################




```

Your successful if the display shows like the following image.<br />

![](./image/execBreakoutSample1.png)

