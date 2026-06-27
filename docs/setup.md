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

## 🧠 2. セットアップを進めるにあたって

セットアップを進めるにあたり、当チームでは以下の2つの原則を大切にしています。

> [!TIP]
> **📖 ライブドキュメントの理念**
> このセットアップガイドは完璧ではありません。ツールのバージョンアップや仕様変更により、手順が古くなっている可能性があります。
> もし動かないコマンドや古い記述、より効率的な設定方法を見つけたら、**あなた自身の手でこのドキュメントを修正し、プルリクエストを出してください**。それがあなたの最初のチーム貢献（Small Win）になります！

> [!IMPORTANT]
> **🤖 15分ルールとAIの活用（AIと人間の役割分離）**
> セットアップ中にエラーや不明な点に遭遇した場合は、以下のステップで解決を試みてください：
> 1. エラーログや疑問点を、インストールする **Claude Code** などのAIアシスタントに貼り付けて相談・調査する（自律的な解決の試み）。
> 2. **15分間** 調べても解決の糸口が見つからない場合は、それ以上一人で抱え込まず、すぐにトレーナーやメンター、あるいはSlackのチャンネルで質問してください。
>
> 基礎的なエラー解決や個別ツールの使用法はAIがサポートし、チーム特有のコンテキストやクリティカルな問題は人間（チームメンバー）がサポートするという役割分担を推奨しています。

---

## 💻 3. PCの初期設定 (macOS前提)

> [!NOTE]
> チームでは主に macOS を使用しています。Windows や Linux を使用する場合はメンターに相談してください。

### Homebrew のインストール
パッケージ管理ツールである [Homebrew](https://brew.sh/) をインストールします。

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Git の基本設定
Gitの基本設定を行います。社内用のメールアドレスを使用してください。

```bash
git config --global user.name "[お名前]"
git config --global user.email "[社内メールアドレス]"

# 改行コードの自動変換を防ぐ（Mac向け推奨設定）
git config --global core.autocrlf input

# push 時に現在のブランチと同名のリモートブランチへ送る設定
git config --global push.default current

# おすすめエイリアスの登録（任意設定）
git config --global alias.co checkout  # co で checkout
git config --global alias.br branch    # br で branch
git config --global alias.ci commit    # ci で commit
git config --global alias.st status    # st で status
git config --global alias.di diff      # di で diff
git config --global alias.graph "log --graph --date=short --decorate=short --pretty=format:'%C(yellow)%h%Creset %C(green)%ad%Creset %s %C(red)%d%Creset %C(bold blue)[%an]%Creset'" # コミット履歴をグラフ付きで綺麗に表示
```

### Spotlight のクリップボード履歴の有効化 (macOS推奨)
macOSの標準機能として、Spotlightからクリップボードの履歴を呼び出せるよう設定します。

1. 画面左上の **Appleメニュー（）** ＞ **「システム設定」** を開きます。
2. サイドバーから **「Spotlight」** を選択します。
3. 画面を下までスクロールし、**「クリップボードからの結果」** をオンにします。
4. （任意）履歴の保存期間（30分、8時間、7日間など）を用途に合わせて選択します。

> [!TIP]
> **使い方**：
> `Command` ＋ `Space` でSpotlightを開き、続けて `Command` ＋ `4` を押すとクリップボード履歴の一覧が表示されます。項目を選択して `Command` ＋ `V` で貼り付けることができます。

### キーボードとトラックパッドのカスタマイズ (推奨)
開発効率向上のため、macOSの基本操作設定をカスタマイズします。

#### 1. キーリピート速度の高速化
コード編集やカーソル移動をスムーズにするために設定します。
- 「システム設定」＞「キーボード」を開きます。
- **キーリピート速度** を「最も速い（右端）」に設定します。
- **リピート入力認識までの時間** を「最も短い（右端）」に設定します。

#### 2. Caps Lock キーを Control に変更
ショートカットキー（`Control + C` 等）を入力しやすくするために変更します。
- 「システム設定」＞「キーボード」を開きます。
- **キーボードショートカット...** ボタンをクリックします。
- サイドバーの **修飾キー** を選択します。
- **Caps Lock (⇪) キー** の選択肢から **^ Control** を選び、「完了」をクリックします。

#### 3. 3本指のドラッグの有効化
ドラッグ操作をスムーズにするために設定します。
- 「システム設定」＞「アクセシビリティ」を開きます。
- 「モーター（物理的動作）」カテゴリにある **ポインタコントロール** をクリックします。
- **トラックパッドオプション...** ボタンをクリックします。
- **ドラッグにトラックパッドを使用** をオンにし、ドラッグスタイルで **3本指のドラッグ** を選択して「OK」をクリックします。

#### 4. タップでクリックの有効化
トラックパッドを物理的に押し込まずに、軽くタップするだけでクリックできるように設定します。
- 「システム設定」＞「トラックパッド」を開きます。
- 「ポイントとクリック」タブ内にある **タップでクリック** をオンにします。

### Shell環境の構築 (oh-my-zsh)
ターミナル環境を快適にするため、[oh-my-zsh](https://ohmyz.sh/) をインストールします。

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

> [!WARNING]
> **ローカルツールのPATH設定**
> oh-my-zshのインストールが完了すると `.zshrc` が生成（または上書き）されます。その後、必ず以下のコマンドを実行して、ローカルツールが配置されるディレクトリ（`$HOME/.local/bin`）へのパスを通してください。
> これは、後述の Claude Code などをターミナルから直接実行するために必要です。

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

---

## 🐙 4. GitHub設定 & GitHub CLI の導入

### SSHキーの作成とGitHubへの登録
GitHubと安全に接続するためにSSHキーを作成し、登録します。

1. **SSHキーの生成**（既存のキーがない場合）
   メールアドレス部分はご自身の社内メールアドレスに置き換えてください。
   ```bash
   ssh-keygen -t ed25519 -C "[社内メールアドレス]"
   ```
2. **ssh-agent の起動**
   ```bash
   eval "$(ssh-agent -s)"
   ```
3. **SSH設定ファイル (`~/.ssh/config`) の作成・編集**
   `vi ~/.ssh/config` 等でファイルを開き、以下の内容を記述します。
   ```text
   Host github.com
     AddKeysToAgent yes
     UseKeychain yes
     IdentityFile ~/.ssh/id_ed25519
   ```
4. **秘密鍵を keychain に追加**
   ```bash
   ssh-add --apple-use-keychain ~/.ssh/id_ed25519
   ```
5. **公開鍵をクリップボードにコピー**
   ```bash
   pbcopy < ~/.ssh/id_ed25519.pub
   ```
6. **GitHubに登録**
   ブラウザで [GitHub SSH Settings](https://github.com/settings/keys) を開き、新しいSSHキーを追加して、コピーした公開鍵を貼り付けます。下記のコマンドでも設定ページを直接開くことができます。
   ```bash
   open https://github.com/settings/keys
   ```
7. **接続テスト**
   ```bash
   ssh -T git@github.com
   ```
   `Hi [ユーザー名]! You've successfully authenticated...` と表示されれば成功です。

### GitHub CLI (`gh`) のインストールと認証
コマンドラインからGitHubの操作を効率化するため、GitHub CLIをインストールしてログインします。

```bash
# インストール
brew install gh

# 認証ログイン
gh auth login
```
※ 画面の指示に従ってブラウザ経由で認証を行ってください。

---

## 📦 5. 必要ツールのインストール

開発に必要なGUIアプリケーションやCLIツールをインストールします。

> [!NOTE]
> エディタ、ターミナル、日本語入力などのアプリケーションについては、チームでよく使われている推奨ツールを紹介していますが、これらはあくまで参考情報です。実際には、ご自身が使い慣れているツールを自由にインストールして使用していただいて構いません。

### GUI アプリケーション

- **Google Chrome**  
  [Chrome ダウンロードページ](https://www.google.com/intl/ja_jp/chrome/) からダウンロードしてインストールします。
- **Google 日本語入力 (Google IME)**  
  より快適な日本語入力環境のため、[Google IME](https://www.google.co.jp/ime/) からダウンロードしてインストールします。
- **Ghostty**  
  高速でモダンなターミナルエミュレータです。[Ghostty ダウンロードページ](https://ghostty.org/download) からダウンロードしてインストールします。
- **VS Code (Visual Studio Code)**  
  メインエディタとして使用します。[VS Code ダウンロードページ](https://code.visualstudio.com/) からダウンロードしてインストールします。
- **Slack**  
  社内コミュニケーションツールです。[Slack for Mac ダウンロードページ](https://slack.com/intl/ja-jp/downloads/mac) からダウンロードしてインストールします。
- **Rectangle**  
  キーボードショートカットでウィンドウを整列できるツールです。[Rectangle ダウンロードページ](https://rectangleapp.com/) からダウンロードしてインストールします。
- **Sequel Ace**  
  データベースを操作するためのGUIクライアントツールです。[Sequel Ace 公式サイト](https://sequel-ace.com/) からダウンロードするか、下記コマンドでインストールしてください。
  ```bash
  brew install --cask sequel-ace
  ```
- **Docker Desktop**  
  ローカルの開発用コンテナ環境を動かすためにインストールします。[Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/) からダウンロードしてインストールします。
  
  インストール完了後、Docker Desktop アプリを起動し、ターミナルで以下を実行して正常に認識されているか確認します。
  ```bash
  docker version
  docker compose version
  ```

### AIバディ (Claude Code)
日常の開発やエラー解決をサポートしてくれるAIコマンドラインツール [Claude Code](https://claude.ai/install.sh) をインストールします。

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### AWS CLI
AWSのサービスをコマンドラインから操作するための [AWS CLI](https://aws.amazon.com/cli/) をインストールします。

```bash
# インストール
brew install awscli

# バージョンの確認
aws --version
```

#### 認証情報（アクセスキー）の設定

AWS CLI を使用するための基本的な認証設定を行います。
詳細な値については、社内の管理者やメンターから取得してください。

```bash
aws configure
# プロンプトに従って入力します
# AWS Access Key ID [None]: [あなたのアクセスキー]
# AWS Secret Access Key [None]: [あなたのシークレットキー]
# Default region name [None]: ap-northeast-1
# Default output format [None]: json
```

---

## 🛠️ 6. ランタイム環境の構築 (mise)

プロジェクトで使用する Node.js や PHP のバージョン管理には、複数ランタイムを一括管理できる [mise](https://mise.jdx.dev/) を使用します。

### 1. mise のインストールと有効化

```bash
# インストール
brew install mise

# zshへのアクティベート設定追加
echo 'eval "$(mise activate zsh)"' >> ~/.zshrc

# 設定をシェルに反映（またはターミナルを再起動）
source ~/.zshrc

# インストールの確認
mise -v
```

### 2. Node.js のセットアップ
プロジェクト指定の Node.js バージョンをグローバルで使用するように設定します。

```bash
# Node.js 26.4.0 のインストールとグローバル設定
mise use --global node@26.4.0

# バージョンの確認
node -v
```

### 3. PHP のセットアップ
PHPのビルドに必要な依存パッケージを Homebrew でインストールした上で、PHPをセットアップします。

```bash
# 1. 必要な依存ライブラリのインストール
brew install pkgconf autoconf gd gmp icu4c zlib curl openssl@3 jpeg-turbo webp freetype oniguruma bison re2c libiconv libpq libpng libsodium libxml2 libzip

# 2. ビルドオプションを指定して PHP 8.5.7 をインストール
PHP_CONFIGURE_OPTIONS="--with-openssl=$(brew --prefix openssl@3) --with-iconv=$(brew --prefix libiconv) --with-icu=$(brew --prefix icu4c) --with-readline=$(brew --prefix readline) --with-pgsql=$(brew --prefix libpq) --with-libxml=$(brew --prefix libxml2)" mise use --global php@8.5.7

# 3. バージョンの確認
php -v
```

---

## 🚀 7. 開発用リポジトリのセットアップ

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
> 具体的な設定値については、社内の管理者またはメンターに確認してください。

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
docker compose up -d
```

---

## ✅ 8. 動作確認

起動後、ブラウザで以下のURLを開き、プロダクトが正常に表示されるか確認してください。

- フロントエンド: `http://localhost:[要記入:ポート番号]` (例: `http://localhost:3000`)
- APIドキュメント (Swagger等): `http://localhost:[要記入:ポート番号]/docs`

正しく画面が表示され、サインインやダッシュボードの表示ができることを確認できたら、開発環境のセットアップは完了です！ 🎉
