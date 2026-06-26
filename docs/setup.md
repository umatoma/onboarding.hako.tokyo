# 🛠️ 開発環境セットアップガイド

このドキュメントでは、開発業務を開始するためのPCセットアップおよび各種アカウントの設定手順を説明します。

---

## 🔑 1. 各種アカウントの設定

まずは以下のサービスのアカウント作成または権限申請を行ってください。
申請方法や管理者は [要記入/管理チームなど] に確認してください。

| サービス名 | 用途 | 申請方法 / リンク | ステータス |
| :--- | :--- | :--- | :---: |
| **GitHub** | ソースコード管理 | [要記入: 申請用フォームなど] | [ ] |
| **Slack** | 社内コミュニケーション | [要記入: 招待用リンクなど] | [ ] |
| **Jira / Confluence** | タスク管理・ドキュメント | [要記入: 申請方法] | [ ] |
| **Google Workspace** | メール・カレンダー等 | [要記入: 管理チームへの申請] | [ ] |
| **AWS / GCP / Azure** | クラウドインフラ（開発環境）| [要記入: 権限申請フォーム] | [ ] |
| **[その他ツール名]** | [用途] | [申請方法] | [ ] |

---

## 💻 2. PCの初期設定 (macOS前提)

> [!NOTE]
> チームでは主に macOS を使用しています。Windows や Linux を使用する場合はメンターに相談してください。

### Homebrew のインストール
パッケージ管理ツールである [Homebrew](https://brew.sh/) をインストールします。

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Git の設定
Gitの基本設定を行います。社内用のメールアドレスを使用してください。

```bash
git config --global user.name "[お名前]"
git config --global user.email "[社内メールアドレス]"
```

### SSHキーの作成とGitHubへの登録
GitHubと安全に接続するためにSSHキーを作成し、登録します。

1. キーの生成（既存のキーがない場合）:
   ```bash
   ssh-keygen -t ed25519 -C "[社内メールアドレス]"
   ```
2. エージェントへの登録と、`~/.ssh/config` の編集。
3. 公開鍵をGitHubに登録する（[GitHub SSH Settings](https://github.com/settings/keys)）。
4. 接続テスト:
   ```bash
   ssh -T git@github.com
   ```

---

## 📦 3. 必要ツールのインストール

開発に必要なランタイムやツールをインストールします。

### インストール推奨ツール
```bash
# 必須パッケージのインストール
brew install git node yarn nvm docker docker-compose

# GUIアプリ（お好みに合わせて）
brew install --cask visual-studio-code google-chrome postman slack
```

> [!TIP]
> Node.js のバージョン管理には `nvm` や `fnm` などの使用を推奨します。
> プロジェクトで指定されている Node.js バージョンは `v[要記入]` です。

---

## 🚀 4. 開発用リポジトリのセットアップ

メインプロダクトのソースコードをローカルに取得し、起動します。

### リポジトリのクローン
適当な作業用ディレクトリ（例: `~/workspace` や `~/src`）にクローンします。

```bash
mkdir -p ~/workspace
cd ~/workspace

# メインリポジトリのクローン
git clone git@github.com:[要記入:組織名]/[要記入:プロジェクト名].git
cd [要記入:プロジェクト名]
```

### 環境変数の設定
環境変数のテンプレート（通常は `.env.example`）をコピーし、必要な値を設定します。

```bash
cp .env.example .env
```
> [!IMPORTANT]
> `.env` に設定するAPIキーや接続情報はセキュリティ上リポジトリに含めないでください。
> 具体的な設定値については、1Passwordの共有ボルト `[要記入: ボルト名]` またはメンターに確認してください。

### 依存関係のインストールと起動

```bash
# 依存パッケージのインストール
npm install # または yarn install, pnpm install

# 開発用サーバーの起動
npm run dev # またはプロジェクトに応じた起動コマンド
```

### データベースやバックエンドサービスの起動
ローカルでDBやモックサービスを動かす必要がある場合：

```bash
# Dockerを使用したDB等の起動
docker-compose up -d
```

---

## ✅ 5. 動作確認

起動後、ブラウザで以下のURLを開き、プロダクトが正常に表示されるか確認してください。

- フロントエンド: `http://localhost:[要記入:ポート番号]` (例: `http://localhost:3000`)
- APIドキュメント (Swagger等): `http://localhost:[要記入:ポート番号]/docs`

正しく画面が表示され、サインインやダッシュボードの表示ができることを確認できたら、開発環境のセットアップは完了です！ 🎉
