# 物理演算Sample

## 物理エンジンにオブジェクトを追加する

```lua
physics.addBody(circle, "static", {density = 1, friction = 0.3, bounce = 0.4})
```

円をディフォルトの"dynamic"から"static"に変え、{}の中にオプショナルな物理的条件を入れます。

- - -

## 物理エンジンを開始

```lua
local physics = require("physics")
physics.start()
```

物理エンジンを開始します。

- - -

## 重力を設定する

```lua
physics.setGravity(x、y)
```

ディフォルトの（０,⒐８）から重力を変える時に使います。

- - -

## 物理エンジンを一時停止する

```lua
physics.pause()
```

- - -

## 物理エンジンに入れたオブジェクトを取り除く

```lua
physics.removeBody(object)
```

- - -

## オブジェクトの速さを設定する

```lua
object:setLinearVelocity(x、y)
```

x軸の速さとy軸の速さをかっこに入れて速さを設定します。

- - -

## オブジェクトがスクリーンに出るか

```lua
rect.isVisible = true
```

ブーリアンでコントロールします。