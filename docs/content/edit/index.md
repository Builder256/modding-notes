# Forge Modding Notes の編集方法

## 概要
Forge Modding Notes は、知見の共有を目的としており、内容の更新、誤字脱字の修正、新しいページの追加など、あらゆるコントリビュートを歓迎します。

この Wiki は [MkDocs](https://www.mkdocs.org/) と [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) を使用して構築されており、GitHub 上で管理されています。

??? info "Git や Python をインストールしていない場合"
    Git や Python などのローカル環境がない場合でも、**GitHub のウェブエディタ**を使用して、ブラウザ上だけで手軽に編集やプルリクエストの送信が可能です。

    1.  編集したいページの右上にある **「Edit this page」** アイコン（鉛筆マーク）をクリックします。
    2.  ブラウザ上で直接内容を編集します。
    3.  「Preview」タブで、Markdown の簡易的なレンダリング結果を確認できます。
        *   ※アドモニションなどの MkDocs 固有の機能は正しく表示されない場合があります。
    4.  編集が終わったら、ページ下部の 「Commit changes...」 から変更内容を送信します。
    5.  自動的にフォークとプルリクエストの作成画面へ進みます。

??? tip "ブラウザ上で完全なプレビュー環境を利用したい場合"
    GitHub の **Codespaces** を利用すると、ブラウザ上で VS Code が起動し、Python などの環境構築を自分で行うことなく、本番同様のプレビュー（`mkdocs serve`）を実行できます。
    リポジトリのトップにある、緑色の「Code」ボタンから「Codespaces」タブを選択して作成してください。

---

## 編集の手順（ローカル環境）

### 1. リポジトリの準備

1.  GitHub の [toapuro/modding-notes](https://github.com/toapuro/modding-notes) をフォークします。
2.  フォークしたリポジトリをローカルにクローンします。
    ```bash title="Terminal"
    git clone https://github.com/YOUR_USERNAME/modding-notes.git
    cd modding-notes
    ```

### 2. ローカル環境の構築

プレビューを確認するために、Python をインストールしている必要があります。

1.  必要なパッケージをインストールします。
    ```bash title="Terminal"
    pip install -r requirements.txt
    ```

### 3. 内容の編集

1.  **Markdown ファイルの作成・編集**:
    - ドキュメントの本体は `docs/content/` ディレクトリ内にあります。
    - 既存のページを更新するか、新しい `.md` ファイルを作成してください。
2.  **ナビゲーションの更新**:
    - 新しいページを追加した場合は、ルートディレクトリにある `mkdocs.yml` の `nav` セクションに、ナビゲーションに表示されるラベルと、それに対応するファイルパスを追記してください。

### 4. ローカルでのプレビュー

編集した内容をブラウザで確認します。

```bash title="Terminal"
mkdocs serve
```

実行後、 `http://127.0.0.1:8000/modding-notes/content/` にアクセスすると、リアルタイムでプレビューが表示されます。

??? bug "リアルタイムプレビューが動作しない場合"
    2026年2月現在、[リアルタイムプレビューが動作しない不具合が報告](https://github.com/squidfunk/mkdocs-material/issues/8478)されています。

    この場合には、`--livereload`オプションを明示的に指定して実行することで、リアルタイムプレビューが動作する可能性があります。

    ```bash title="Terminal"
    mkdocs serve --livereload
    ```

### 5. コミットとプッシュ

変更が完了したら、コミットしてプッシュします。

**コミットメッセージの形式:**
[`CONTRIBUTING.md`](https://github.com/toapuro/modding-notes/blob/master/CONTRIBUTING.md) に基づき、以下の形式を使用してください。

- `Add: <内容>` : ドキュメントの新規追加
- `Update: <内容>` : ドキュメントの更新
- `Fix: <内容>` : 誤字脱字やバグの修正

```bash title="Terminal"
git add .
git commit -m "Update: 編集方法のページを追加"
git push origin main
```

### 6. プルリクエストの作成

GitHub 上でオリジナルのリポジトリに対してプルリクエスト（PR）を作成してください。
未完成の状態でも、「Draft PR」として送っていただければサポートできる場合があります。

---

## 執筆のガイドライン

### 推奨されるスタイル

- **正確性より共有**: 完璧な文章である必要はありません。有用な知見を残すことを優先してください。
- **コードブロック**: 言語名を指定して(例: ` ```java ` )記述してください。可能であれば `title="Filename.java"` のようにタイトルを付けてください。
- **アドモニション（注釈など）**: Material for MkDocs の機能が使用可能です。
  ```markdown
  !!! info "タイトル"
      ここに内容を記述します。
  ```

### 禁止事項

- 他者の著作権を侵害する内容の転載。
- Minecraft の EULA に違反する内容。
