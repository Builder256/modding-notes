# 環境構築

## Intellijのセットアップ

!!! info "エディタについて"
    Eclipse IDEやVS Codeでも開発できますが、この章では触れません。

1. **Intellij IDEAのインストール**

    個人利用なら **Ultimate**ではなく少し下にある {==**Community**==}を選んでください。
    
    [公式ダウンロードページ](https://www.jetbrains.com/ja-jp/idea/download/?section=windows)

2. **日本語化 (任意)**
    
    Intellijを起動してランチャーメニューになったら、サイドバーのPluginsタブから {==Japanese Language Pack==} と検索してインストールします。
    インストール後にIntellijを再起動すれば日本語化が反映されます。
    ![](../assets/intellij/intellij-japanese-ext.png)

3. **Minecraft Developmentプラグインをインストール**

    同じくPluginsタブから {==Minecraft Development==} と検索してインストールし、完了したら一度Intellijを再起動してください。

## 事前知識

スキップしても大丈夫ですが、迷ったときに軽く振り返ってもらえると理解しやすくなります

| 用語        | 備考                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------ |
| Mixin       | これをオンにしない場合、依存関係を設定する時に面倒なので、オンにしておくことをおすすめします。   |
| License     | その Modの著作権の扱い方を宣言するもので、依存関係を設定する時、確認する必要があります。        |
| Group ID    | パッケージの指定。ドメインを逆に書く。`io.github.作者名.プロジェクト名` のような形式がいいかも。 |
| Package     | パッケージ。クラスをグループで管理できる仕組みで、実態としてはフォルダとほぼ同じ。               |
| Artifact ID | 基本的にModのIDを書いておく。                                                                |
| Class       | Javaでコードを書く基本単位。1クラス1ファイルで機能ごとに分割できる                           |

| プラットフォーム | 備考                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------ |
| Neoforge         | 1.20.4 以降はこちら。1.20.4 移行のバージョンを開発する、ほとんどの開発者が移行済み。 |
| Forge            | 1.20.4 未満ならこちら                                                                |

1.20.1は特別にNeoforgeとForgeどちらも対応しています

## Mod開発環境のセットアップ

いくつか方法があります

Neoforgeであれば[1, (NeoForge/Fabric) Modジェネレータの利用](#1-neoforgefabricmodジェネレータの利用)を推奨

Fabricであれば[1, (NeoForge/Fabric) Modジェネレータの利用](#1-neoforgefabricmodジェネレータの利用)を推奨

Forgeであれば[4, (NeoForge/Forge/Fabric) プラグイン経由で生成](#4-neoforgeforgefabricプラグイン経由で生成)を推奨

### 1, (NeoForge/Fabric) Modジェネレータの利用

Neoforge (1.20.4 以降)  
[NeoForge Mod Generator](https://neoforged.net/mod-generator/)

Fabricならこちら  
[Fabric Template](https://fabricmc.net/develop/template/)

### 2, (NeoForge) テンプレートをクローン

[NeoForge テンプレート一覧](https://github.com/orgs/NeoForgeMDKs/repositories)

ここにあるリポジトリの中から対象のバージョンを探して、
右上の Code->Download ZIP からダウンロード・解凍し、build.gradle を開けば IDE が立ち上がるはずです。

!!! tip
    `git clone --depth 1 https://github.com/~~` でクローンしても大丈夫です(depth=1 は不要なコミットを省くため)。

### 3, (Forge) Forge MDK[^1]の利用

[Forge MDK](https://files.minecraftforge.net/net/minecraftforge/forge/)

こちらからバージョンを選択して MDK をダウンロードし解凍、build.gradle を開きます。

!!! tip
    LatestとRecommendedの違いは基本的にあまりありません。どちらでもよし。

[^1]: MDKはMod Developer Kitの略で、いわゆるテンプレートです。

### 4, (NeoForge/Forge/Fabric) Intellijプラグイン経由で生成

プロジェクトを新規作成するとき左下にあるジェネレータから Minecraft を選択し、各項目を入力して作成を押してください。

!!! note
    JDKの指定が必要な場合は [Java JDK](#java-jdk)を参考にしてみてください。

## Java JDK

JDKはJavaを実行するためのキットのようなもの、と捉えてもらえればOKです。

以下のテーブルのように、マイクラバージョンごとにJDKが異なり、基本的に開発環境もこれに合わせます。

| MC バージョン | JDK バージョン |
| ------------- | -------------- |
| 1.16.x        | JDK 8          |
| 1.17.x        | JDK 16         |
| 1.18.x        | JDK 17         |
| 1.19.x        | JDK 17         |
| 1.20.x        | JDK 17         |
| 1.21.x        | JDK 21         |

### ダウンロード

Intellijであれば、左上の ≡ メニュー->ファイル->プロジェクト構成->プロジェクトと進み、SDK[^2]を指定できると思いますが、そこで{==JDKのダウンロード...==}を選択することでダウンロードできます。

![JDKのダウンロード](../assets/intellij/jdk-download.png)

バージョンは先程のテーブルを参考に設定してください。

ベンダー[^3]の選択ができると思いますが、特にこだわりがなければ{==JetBrains Runtime==}がおすすめです。

!!! info
    Jetbrains Runtimeではホットスワップという、実行中にコードを変更して適応させられる機能が使えます。

また、たまに使うのでJava(JDK)をダウンロードしていない場合は、一応ダウンロードしておきましょう。

少ないですがいくつかベンダーを紹介しておきます。

- [Adoptium](https://adoptium.net/temurin/releases)

- [OpenJDK](https://jdk.java.net/25/)

[^2]: JavaではJDKのこと
[^3]: Java関連のベースキットを提供する企業やサービス

## テンプレートの編集(2,3の方法でセットアップした場合のみ)
`gradle.properties`に`mod_id`や、`mod_name`等があるため、それを適切な値に変更してください

分からない用語は[#用語解説](#事前知識)を参照してください

## ビルド・実行の方法

右側にある gradle アイコンを押して

![](../assets/intellij/gradle.png)

ビルドであれば Tasks->build->build。

実行であれば forgegradle runs->runClientにあるかと思います

初心者向けの解説は一旦ここまでです。