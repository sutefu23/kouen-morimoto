---
marp: true
theme: kouen
class: lead
paginate: true
backgroundColor: white
---

# はじめての Claude Code

---
<style scoped>
session {
  font-size: 24px;
}
p{
  line-height: 1em;
}
</style>

# Claude Codeとは

Anthropic社が開発したCLIツール

### 何が嬉しいのか

- 環境を選ばずインストールして動作してくれる。
- コード全体を理解しながら動作してくれる
- よって応用範囲が広く、自由度も高い。
- CLIの特徴を活かして複数立ち上げての並行処理などが可能

---

### **Claude Code の活用シーン**

1. **新規機能の実装** - 要件を伝えるだけで設計から実装まで
2. **バグ修正** - エラーログから原因特定と修正案の提示
3. **リファクタリング** - コード品質向上の自動提案
4. **テストコード生成** - 実装に合わせたテストの自動作成
5. **ドキュメント作成** - コードからREADMEや仕様書を生成
6. **技術調査** - 新しいライブラリやフレームワークの学習支援

---
<style scoped>
section{
  font-size:2em;
}
</style>

# インストール

2025年11月より次で説明する各OSに対応したネイティブインストールが推奨

### Homebrew (macOS, Linux):
```bash
brew install --cask claude-code
```

### macOS, Linux, WSL:
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### Windows PowerShell:
```bash
irm https://claude.ai/install.ps1 | iex
```

---

# 料金体系２つ

<i>**※サブスクのClaude.aiアカウントとClaude Consoleアカウントは別物なので注意。**</i>

### - **サブスクリプションプラン**

  Pro (20ドル／月)、Max5x（100ドル／月）、 Max 20x（200ドル／月）


### - **従量課金プラン**

**Sonnet 4.5**：

入力100万トークンあたり$3、出力100万トークンあたり$15

**Opus 4.1**：

入力100万トークンあたり$15、出力100万トークンあたり$75


---

# 立ち上げ

```
claude
```

```
> /init
```

CLAUDE.mdが生成される。
これを「メモリ」といいClaudeの記憶のような役割を担う。
本来Claude Codeでは会話セッション（=ユーザーとのやり取り）単位でしか記憶を保持しない。

ここには技術要件やコード全体の仕様などが記載される。プログラマーにとってのREADMEのようなもの。

必ずコンテキストに含まれる。

---

# 設定ファイル

`.claude/settings.local.json`
ここにファイルの編集許可、実行できるツールの設定
対話モードで回答すると自動で入ります。

---

# Claude Codeの4つのモード

Claude Codeには4つの動作モードがあります。

| モード | 説明 |
| ---- | ---- |
| default| 	デフォルトの動作。各ツールの初回使用時に権限の許可を求める |
| acceptEdits| 	セッション中のファイル編集権限を自動的に受け入れる |
| plan	| Claudeが分析と計画策定のみ行う。ファイルの変更やコマンドの実行は行わない。 |
| bypassPermissions	| すべての権限プロンプトをスキップする（安全な環境が推奨） |
--- 

## **defaultモード**

何も設定しない場合は、勝手にファイルを編集しない。
する場合は必ずユーザーに許可を求める。

## **acceptEdits**

Claudeに編集を許可するモード。
defaultモードの時、ファイルを編集する際に「Claudeにファイルの編集を許可するか？」と聞かれて「2. Yes, and don't ask again this session (shift+tab) 」（このセッションでは再び聞かない）を選択するとacceptEditモードになります。

`Shift + Tab`を1回押すことでもこのモードになります。


--- 

## **planモード**

対話モードで`Shift+Tab`をさらに押すと発動。枠線が緑になる。
Claudeはファイルを編集せず、実行計画や分析だけを行います。

「ファイルを弄らせずアドバイスだけをもらいたい」とか「今考えてる機能を実装した時に、どんな実装になりそうか教えてほしい」という時には向いています。
Claudeがプランを立てた後は「Ready to code?」と聞かれ選択肢が提示されます。

---

## **bypassPermissionsモード**

Claudeにコマンド実行のすべての権限を与える。
唯一立ち上げ時に、

```bash
claude --dangerously-skip-permissions
```
と引数を指定することで発動。

強力だが実装の詳細も見えづらく、危険な動作をしてもStopできないため、適切にリポジトリ管理した上で、Docker環境やSandboxモードで動かすことを推奨。

普段使いで言えば、どちらかと言えばlintエラーの修正や定型コードの生成などの暴走リスクの少ないワークフローに適しています。

---

# MCPサーバーとは

- MCPはLLMと外部ツールがやり取りするための通信規格

- MCPサーバーはその通信規格を使って外部ツールやデータへのアクセスを提供
結果的に拡張機能として様々な能力をClaudeに与える

  
## 何が嬉しいの？

Goolg DriveやGitHub、Jira、Notionなどの読込、書き込みなど、外部サービスと連携可能

---

# MCPサーバーの設定

```
claude mcp add <MCPサーバーの名前> <MCPサーバーのURLや立ち上げコマンド>
```

---

# おすすめMCPサーバー

### - **Context7**
### - **Playwright**
### - **Serena**

---

# Context7

Context7は各ライブラリやフレームワーク、APIドキュメントなどの技術ドキュメントをClaudeに提供し、コード生成や修正、レビューの精度を向上させる。

### - **インストール方法**
```bash
claude mcp add context7 -s user -- npx -y @upstash/context7-mcp
```

#### - **使い方**
プロンプトで何かライブラリを使いたいときに`use context7`と言って呼び出す
```bash
> TODOアプリをNext.jsのApp Routerを使って作ってください。データはローカルに保存してください。 use context7
```

---

## **Playground**

フロントの表示確認、エラー確認、動作確認など、Claude Codeに目を付ける事ができる。

## - **インストール方法**
```bash
claude mcp add Playwright npx @Playwright/mcp@latest
```

## - **使い方**
「PlaywrightMCPサーバーで確認して、直るまで修正を繰り返して」と伝えると効果的。Consoleエラーなども取得可能。

最近はChrome MCPサーバーも人気。Chrome MCPはログインセッションなども引き継げる。

---

## **Serena**
SerenaはIDEと同じようにLSP（Language Server Protocol）を提供することで（脚注）、Claudeに対してより深いコード理解をもたらす。

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```bash
claude mcp add serena \
  -- uvx --from git+https://github.com/oraios/serena serena-mcp-server \
  --context ide-assistant --project $(pwd)
```

## 使い方

プロジェクトにインストールすればClaudeを立ち上げた際に自動で立ち上がる。

---

# インフラを任せるとClaude Codeは最強

`gh`コマンド、`gcp`コマンド、`aws`コマンドなどはインストールして認証は通しておくべき。

インフラ構築や管理をClaude Codeに任せることができる。またサーバーログを自身でアクセスして分析させることで、効果的なデバッグができる。

---

# 並列実行

CLIの特性を活かして、複数のClaude Codeセッションを並列で実行することも可能。

Git Worktreeを使って、異なるタスクを同時に進行できる。

## Git Worktreeとは
Git Worktreeを使うと追加のcloneをせずに、同じ.gitを共有して複数の作業環境を持てるようになる。
`git worktree add -b ./feature-x feature-x`などのコマンドで特定のディレクトリに特定のブランチをチェックアウト可能。

---

## **平行処理のコツ**

並行処理なのでどうしてもコードにコンフリクトが生じることがある。

違うセッションのClaudeは別人格のようなものなので、なるべくお互いの作業を被らせないことが基本的なコツ。

そのためフロントエンド、バックエンド、テスト、インフラ、などそれぞれ担当する作業を分けた方が良い。
たとえば一人にはフロントエンドをやらせる、一人にはバックエンドをやらせる、など。
特に立ち上がり時などは力を発揮する。

---
<style scoped>
section {
  text-align: center;
}

</style>
# これを100倍詳しく書いたのが<br><br>「Claude CodeによるAI駆動開発入門」

![./image/book.png](./image/book.png)