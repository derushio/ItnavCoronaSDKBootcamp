# 画面遷移サンプル全体コード

## main.lua

```lua
-----------------------------------------------------------------------------------------
--
-- main.lua
--
-----------------------------------------------------------------------------------------

-- グローバル変数(プロジェクト内で有効な変数)
composer = require("composer")
TopScene = require("TopScene")
MainScene = require("MainScene")

-- 横幅と縦幅
_W = display.contentWidth
_H = display.contentHeight

-- TopSceneに画面遷移
composer.gotoScene(TopScene.name, nil, 0)
```

- - -

## TopScene.lua

```lua
---------------------------------------------------------------------------------
--
-- TopScene.lua
--
---------------------------------------------------------------------------------

local this = composer.newScene()
this.name = "TopScene"

-- ########## Sceneライフサイクルメソッド #######################
-- 画面生成時のハンドラ
function this:create(event)
	local sceneGroup = this.view

	-- オブジェクトを配置
	this.background = display.newRect(sceneGroup, _W/2, _H/2, _W, _H)
	this.background:setFillColor(0.5, 0.5, 0.5)
	this.nameText = display.newText({
		parent = sceneGroup,
		text = this.name,
		x = _W/2,
		y = _H/2,
		width = _W,
		height = 100,
		font = native.systemFont,
		fontSize = 60,
		align = "center"
	})
	this.nameText:addEventListener("tap", this.onNameTextTap)
end

-- 画面表示時のハンドラ
function this:show(event)
	local phase = event.phase
	
	if "did" == phase then
	end
end

-- 画面非表示時のハンドラ
function this:hide(event)
	local phase = event.phase
	
	if "will" == phase then
	end
end

-- 画面破壊時のハンドラ
function this:destroy(event)
	this.nameText:removeEventListener("tap", this.onNameTextTap)
	this.removeAll()	
end
-- ########## Sceneライフサイクルメソッド #######################



-- ########## Sceneメソッド #####################################
this.removeAll = function()
	local sceneGroup = this.view
	for i = sceneGroup.numChildren, 1, -1 do
		local child = sceneGroup[i]
		child.parent:remove(child)
		child = nil
	end
end

this.onNameTextTap = function(event)
	-- MainSceneに画面遷移
	composer.gotoScene(MainScene.name, "crossFade", 500)
	-- アニメーション時間を考慮した削除
	timer.performWithDelay(500, 1, function()
		composer.removeScene(this.name)
	end)
end
-- ########## Sceneメソッド #####################################



-- ########## EventListener登録 #################################
this:addEventListener("create", this)
this:addEventListener("show", this)
this:addEventListener("hide", this)
this:addEventListener("destroy", this)
-- ########## EventListener登録 #################################

return this
```

- - -

## MainScene.lua

```lua
---------------------------------------------------------------------------------
--
-- MainScene.lua
--
---------------------------------------------------------------------------------

local this = composer.newScene()
this.name = "MainScene"

-- ########## Sceneライフサイクルメソッド #######################
-- 画面生成時のハンドラ
function this:create(event)
	local sceneGroup = this.view

	-- オブジェクトを配置
	this.background = display.newRect(sceneGroup, _W/2, _H/2, _W, _H)
	this.background:setFillColor(0.0, 0.5, 0.5)
	this.nameText = display.newText({
		parent = sceneGroup,
		text = this.name,
		x = _W/2,
		y = _H/2,
		width = _W,
		height = 100,
		font = native.systemFont,
		fontSize = 60,
		align = "center"
	})
	this.nameText:addEventListener("tap", this.onNameTextTap)
end

-- 画面表示時のハンドラ
function this:show(event)
	local phase = event.phase
	
	if "did" == phase then
	end
end

-- 画面非表示時のハンドラ
function this:hide(event)
	local phase = event.phase
	
	if "will" == phase then
	end
end

-- 画面破壊時のハンドラ
function this:destroy(event)
	this.nameText:removeEventListener("tap", this.onNameTextTap)
	this.removeAll()	
end
-- ########## Sceneライフサイクルメソッド #######################



-- ########## Sceneメソッド #####################################
this.removeAll = function()
	local sceneGroup = this.view
	for i = sceneGroup.numChildren, 1, -1 do
		local child = sceneGroup[i]
		child.parent:remove(child)
		child = nil
	end
end

this.onNameTextTap = function(event)
    -- TopSceneに画面遷移
	composer.gotoScene(TopScene.name, "fade", 500)
    -- アニメーション時間を考慮した削除
	timer.performWithDelay(500, 1, function()
		composer.removeScene(this.name)
	end)
end
-- ########## Sceneメソッド #####################################



-- ########## EventListener登録 #################################
this:addEventListener("create", this)
this:addEventListener("show", this)
this:addEventListener("hide", this)
this:addEventListener("destroy", this)
-- ########## EventListener登録 #################################

return this
```