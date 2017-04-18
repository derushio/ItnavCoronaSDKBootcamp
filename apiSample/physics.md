# 物理演算Sample

## 物理エンジンにオブジェクトを追加する

```lua
addBody(オブジェクト, 物理エンジン上の振る舞い, 物理的条件)
```

```lua
physics.addBody(circle, "static", {density = 1, friction = 0.3, bounce = 0.4})
```

circle(円だと仮定します)を `"static"(動かないオブジェクト)` で物理エンジンに登録します。  
動くオブジェクトの場合は `"dynamic"` を指定します。

参考
CoronaSDK Reference[physics.addBody]

[https://docs.coronalabs.com/api/library/physics/addBody](https://docs.coronalabs.com/api/library/physics/addBody.html)

---

## 物理エンジンを開始

```lua
local physics = require("physics")
physics.start()
```

物理エンジンを開始します。

参考
CoronaSDK Reference[start]

[https://docs.coronalabs.com/api/library/physics/start](https://docs.coronalabs.com/api/library/physics/start.html)

---

## 重力を設定する

```lua
physics.setGravity(x、y)
```

デフォルトの `(0, 9.8)` から重力を変える時に使います。

参考
CoronaSDK Reference[setGravity]
[https://docs.coronalabs.com/api/library/physics/setGravity](https://docs.coronalabs.com/api/library/physics/setGravity.html)

---

## 物理エンジンを一時停止する

```lua
physics.pause()
```

CoronaSDK Reference[pause]

[https://docs.coronalabs.com/api/library/physics/pause](https://docs.coronalabs.com/api/library/physics/pause.html)

---

## 物理エンジンに入れたオブジェクトを取り除く

```lua
physics.removeBody(object)
```

参考
CoronaSDK Reference[removeBody]
[https://docs.coronalabs.com/api/library/physics/removeBody](https://docs.coronalabs.com/api/library/physics/removeBody.html)

---

## オブジェクトの速さを設定する

```lua
object:setLinearVelocity(x、y)
```

x軸の速さとy軸の速さをかっこに入れて速さを設定します。

参考
CoronaSDK Reference[setVelocity]

[https://docs.coronalabs.com/api/type/Body/setLinearVelocity](https://docs.coronalabs.com/api/type/Body/setLinearVelocity.html)

---

## オブジェクトがスクリーンに出るか

```lua
rect.isVisible = true
```

ブーリアンでコントロールします。

参考
CoronaSDK Reference[isVisible]

[https://docs.coronalabs.com/api/type/DisplayObject/isVisible](https://docs.coronalabs.com/api/type/DisplayObject/isVisible.html)

---

## 衝突判定

```lua
function onCollision(event)
    event.other.isVisible = false
end

ball:addEventListener("collision", onCollision)
```

`ball` と衝突したオブジェクトを見えなくします。  
衝突したオブジェクトは `event.other` で取ることができます。

参考
CoronaSDK Reference[collision]

[https://docs.coronalabs.com/api/event/collision/index](https://docs.coronalabs.com/api/event/collision/index.html)

