# 2. シーンを作ろう

## TopScene.luaファイルを作ろう
使用しているテキストエディタ、またはファイルエクスプローラーから `TopScene.lua` を作成しましょう。

- - -

## Sceneを作ろう
CoronaSDKでは、以下のコードでScene(画面)を定義できます。

```lua
local this = composer.newScene()
this.name = "TopScene"
```

`TopScene.lua` の一番上に書きましょう。


CoronaSDK Reference[newScene]

[https://docs.coronalabs.com/api/library/composer/newScene](https://docs.coronalabs.com/api/library/composer/newScene.html)


---

## Sceneライフサイクルを定義しよう
Sceneにはライフサイクル(Sceneの状態の遷移)があり、Sceneを作る時、削除する時などの挙動を定義する必要があります。  
以下のコードで定義できます。

```lua
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
```

CoronaSDK Reference[newRect]

[https://docs.coronalabs.com/api/library/display/newRect](https://docs.coronalabs.com/api/library/display/newRect.html)


先程書いたSceneを定義したコードの下に書いてみましょう。


---

## Scene内で使うメソッドを定義してみよう
ライフサイクルメソッド以外にも、Scene内で使いたいメソッドがたくさんあるはずです。  
そんなときは以下のように定義できます。

```lua
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
```

CoronaSDK Reference [gotoScene]

[https://docs.coronalabs.com/api/library/composer/gotoScene](https://docs.coronalabs.com/api/library/composer/gotoScene.html)

CoronaSDK Reference [performWithDelay]

[https://docs.coronalabs.com/api/library/timer/performWithDelay](https://docs.coronalabs.com/api/library/timer/performWithDelay.html)


Sceneのライフサイクルを定義したコードの下に書いてみましょう。

---

## Sceneのライフサイクルを登録しましょう
Sceneの仕様上、定義したライフサイクルを登録する必要があります。  
以下のコードで登録できます。

```lua
-- ########## EventListener登録 #################################
this:addEventListener("create", this)
this:addEventListener("show", this)
this:addEventListener("hide", this)
this:addEventListener("destroy", this)
-- ########## EventListener登録 #################################
```

Sceneのメソッドを定義したコードの下に書いてみましょう。

---

## Sceneをファイルの外に返しましょう
composerを利用する仕様上、ファイルの外にSceneを返す必要があります。  
`TopScene.lua` の最後に以下のコードを書きましょう。

```lua
return this
```

---

## 今回のセクションまでで書いたコード

### main.lua

```lua
-----------------------------------------------------------------------------------------
--
-- main.lua
--
-----------------------------------------------------------------------------------------

-- Your code here
```

### TopScene.lua

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