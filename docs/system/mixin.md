# Mixin

MinecraftまたはMODのコードを一部改変できる仕組みです。

## 概要

実際に何ができるかコードで解説します。

Mixinの対象クラス
```java title="SomethingLogic.java"
class SomethingLogic {
    public void process() {
        System.out.println("Proceed");
    }
}
```

Mixinクラス
``` java title="MixinSomethingLogic.java"
// リマッピングオフでSomethingLogicにMixin
@Mixin(value = SomethingLogic.class, remap = false)
public class MixinSomethingLogic {

    // メソッドの最初に注入
    @Inject(method = "process()V", at = @At("HEAD"))
    private void onProcess(CallbackInfo ci) {
        System.out.println("Injected");
    }
}
```

このMixinがSomethingLogicに適応されると、**概念的には**[^1]以下のようになります。
``` java title="SomethingLogic(Injected).java"
class SomethingLogic {
    public void process() {
        onProcess(new CallbackInfo(...))
        System.out.println("Proceed");
    }

    private void onProcess(CallbackInfo ci) {
        System.out.println("Injected");
    }
}
```
[^1]: 実際はonProcessのメソッド名やアノテーションなどが異なる。

## Mixinセットアップ

以下を`build.gradle`の冒頭に追加。
```gradle title="build.gradle"
buildscript {
    repositories {
        maven { url = 'https://repo.spongepowered.org/repository/maven-public/' }
        mavenCentral()
    }
    dependencies {
        classpath 'org.spongepowered:mixingradle:0.7-SNAPSHOT'
    }
}
```

以下を `plugins {}` ブロックの下に追加。
```diff title="build.gradle"
plugins {
    ...
}
+ apply plugin: 'org.spongepowered.mixin'
```

以下を`build.gradle`の`dependencies {}`ブロックの下に追加。
```diff title="build.gradle"
dependencies {
+    annotationProcessor 'org.spongepowered:mixin:0.8.5:processor'
}
```

以下を`src/main/resources/<modid>.mixins.json`に
```json title="<modid>.mixins.json"
{
  "required": true,
  "minVersion": "0.8",
  "package": "<groupId>.mixin",
  "compatibilityLevel": "JAVA_17",
  "mixins": [],
  "client": [],
  "server": [],
  "injectors": {
    "defaultRequire": 1
  }
}
```
`<modid>`や`<groupID>`は適切なものに置き換えてください。

次に、`build.gradle`の`minecraft {}`ブロックの下に以下を追加。
```gradle
mixin {
    add sourceSets.main, "${mod_id}.refmap.json"

    config "${mod_id}.mixins.json"
}
```
`${mod_id}`はそのままで大丈夫です

## Mixinの使い方

実践的なコードですが、以下が参考になるかと思います。

[Mixin Examples - Fabric Wiki](https://wiki.fabricmc.net/tutorial:mixin_examples)

まずどこにコードを注入するか、どこのコードを改変するかを指定するための@Atを解説します

### @At

`@At` はどこにコードを注入するかを指定します。

`@At("HEAD")`のように使用します

以下が主な値です。(value引数)

- `HEAD`: メソッドの最初
- `TAIL`: メソッドの最後
- `RETURN`: `return` 文の前
- `INVOKE`: 特定のメソッドを呼び出す前
- `FIELD`: フィールドアクセス
- `STORE`: 変数代入 (`@ModifyVariable`のみ)
- `LOAD`: 変数の取得 (`@ModifyVariable`のみ)

