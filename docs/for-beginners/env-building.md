# 環境構築

### Intellij のセットアップ

!!! info "エディタ"
    Eclipse IDE や VS Code でも開発できますが、この章では触れません。

1. **Intellij IDEA のインストール**

    個人利用なら **Ultimate** ではなく少し下にある **Community** を選んでください。  
    [公式ダウンロードページ](https://www.jetbrains.com/ja-jp/idea/download/?section=windows)

2. **日本語化 (任意)**
    
    Intellij を起動してランチャーメニューになったら、サイドバーの Plugins から Japanese Language Pack を検索してインストールします。  
    インストール後に Intellij を再起動すれば日本語化が反映されます。  
    ![](../assets/intellij-japanese-ext.png)

3. **Minecraft Development プラグインをインストール**

    同じく Plugins から Minecraft Development というプラグインをインストールし、完了したら一度 Intellij を再起動してください。

### 事前知識

スキップしても大丈夫ですが、迷ったときに軽く振り返ってもらえると理解しやすくなります

| 用語        | 備考                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------ |
| Mixin       | 練習のために有効化できるようにしておいたほうがいいかもしれない                                   |
| License     | ライセンス。mod 公開時に色々気をつけないといけない。ドキュメントの注意事項 →MOD 公開で解説       |
| Group ID    | パッケージの指定。ドメインを逆に書く。`io.github.作者名.プロジェクト名` のような形式がいいかも。 |
| Package     | パッケージ。クラスをグループで管理できる仕組みで、フォルダのようなもの                           |
| Artifact ID | 小文字で mod 名を入れておけば困らない                                                            |
| Class       | Java でコードを書く基本単位。1 クラス 1 ファイルで機能ごとに分割できる                           |

| プラットフォーム | 備考                                                                         |
| ---------------- | ---------------------------------------------------------------------------- |
| Neoforge         | 1.20.2 以降はこちら。ほとんどの開発者が移行済みで、1.20.1 版も用意されている |
| Forge            | 1.20.4 未満ならこちら                                                        |


1.20.1 は特別に neoforge と forge どちらも対応しています

### Mod 開発環境のセットアップ

いくつか方法があります

Neoforge であれば[1, (NeoForge/Fabric) mod ジェネレータの利用](#1-neoforgefabric-mod-ジェネレータの利用)を推奨

Fabric であれば[1, (NeoForge/Fabric) mod ジェネレータの利用](#1-neoforgefabric-mod-ジェネレータの利用)を推奨

Forge であれば[4, (NeoForge/Forge/Fabric) プラグイン経由で生成](#4-neoforgeforgefabric-プラグイン経由で生成)を推奨

#### 1, (NeoForge/Fabric) mod ジェネレータの利用

Neoforge (1.20.4 以降)  
[NeoForge Mod Generator](https://neoforged.net/mod-generator/)

Fabric ならこちら  
[Fabric Template](https://fabricmc.net/develop/template/)

#### 2, (NeoForge) テンプレートをクローン

[NeoForge テンプレート一覧](https://github.com/orgs/NeoForgeMDKs/repositories)

ここにあるリポジトリの中から対象のバージョンを探して、
右上の Code->Download ZIP からダウンロード・解凍し、build.gradle を開けば IDE が立ち上がるはずです。

!!! tip
    `git clone --depth 1 https://github.com/~~` でクローンしても問題ありません (depth=1 は不要なコミットを省くため)。

#### 3, (Forge) Forge MDK の利用

[Forge MDK](https://files.minecraftforge.net/net/minecraftforge/forge/)

こちらからバージョンを選択して Mdk をダウンロードし解凍、build.gradle を開きます。

!!! tip
    Latest と Recommended の違いは大きくありません。同じバージョンであれば、使いやすい方を選んで問題ありません。

#### 4, (NeoForge/Forge/Fabric) プラグイン経由で生成

プロジェクトを新規作成するとき左下にあるジェネレータから Minecraft を選択し、各項目を入力して作成を押してください。

!!! note
    JDK の指定が必要な場合は [Java JDK インストール](#java-jdk-インストール) を参考にしてください。

### Java JDK インストール

以下のバージョン表を参考に JDK をインストールしておくと安心です。
JDK は Java を実行するためのキットのようなもの、と捉えてもらえれば OK です

Mineraft バージョンに対応する最小 JDK バージョン

|        |        |
| ------ | ------ |
| 1.16.x | JDK 8  |
| 1.17.x | JDK 16 |
| 1.18.x | JDK 17 |
| 1.19.x | JDK 17 |
| 1.20.x | JDK 17 |
| 1.21.x | JDK 21 |

4 以外でセットアップした方は、左上の ≡ メニューからファイル->プロジェクト構成->プロジェクト->SDK を指定してください。
まだ JDK を入れていない場合は、JDK のダウンロードから対象バージョンを入手して設定すれば問題ありません

### ビルド・実行の方法

右側にある gradle アイコンを押して

![](../assets/gradle.png)

ビルドであれば Tasks->build->build。

実行であれば forgegradle runs->runClientにあるかと思います

初心者向けの解説は一旦ここまでです。