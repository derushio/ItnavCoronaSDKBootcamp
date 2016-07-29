# 3. 物理演算とは

## 物理演算とは
CoronaSDKは物理演算(ボールが地面にぶつかって跳ねる挙動をアプリで再現する等)の機能をもっています。  
物理演算は以下のコードで呼び出すことができます。

```lua
-- 物理演算をするための機能を読み込んで `physics` に入れておく
physics = require("physics")
-- 物理演算を起動する
physics.start(true)
physics.setGravity(0, 0)
```

現状では何も動きませんが、次からのセクションで効果を発揮するのでどんどん進みましょう。

- - -

## セクション中の全文
このセクションで書いたコードの全文は以下になります。

```lua
-- 物理演算をするための機能を読み込んで `physics` に入れておく
physics = require("physics")
-- 物理演算を起動する
physics.start(true)
physics.setGravity(0, 0)
```

画面は以下のようになっていれば成功です。  
まだ前のセクションと同じ画面です。

![](./image/execBreakoutSample2.png)
