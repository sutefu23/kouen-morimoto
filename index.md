---
marp: true
theme: kouen
class: lead
paginate: true
backgroundColor: white
header: "**Claude CodeによるAI駆動開発入門に書けなかったコト**"
---
<script src="https://cdn.tailwindcss.com/"></script>
<script>tailwind.config = { corePlugins: { preflight: false } }</script>

<style scoped>
section{
  text-align:center;
}
</style>

# 「Claude CodeによるAI駆動開発入門」<br>に書けなかったコト


  <img  src="./image/kumai.png" alt="平川の写真" />


---

# 自己紹介

<div class="columns">
  <div>
    <img  src="./image/hirakawa.png" alt="平川の写真" />
  </div>
  <div>
  <p class="text-2xl">
    株式会社en-gine代表。エンジニア歴10年。<br>
    東京と福岡を拠点に、生成AI・クラウドアーキテクチャ・LLMエージェント技術を活用した業務システム・SaaSの設計開発に従事。<br>
    現在は、AIと人間の協働による「AI駆動開発（AI-Driven Development）」の普及を目指し、企業支援・教育活動も行っている。<br>
   「<a target="_blank" href="https://www.amazon.co.jp/dp/4297152754/"><strong class="orange">Claude CodeによるAI駆動開発入門</strong></a>」が技術評論社より12月5日刊行予定。
  </p>
  </div>
</div>

---
# お陰様でAmazonランキング1位獲得
<div class="columns h-100">
  <div>
「ソフトウェア開発・言語」ジャンル1位
「生成AI」ジャンル2位
  </div>
  <div>
    <a target="_blank" href="https://www.amazon.co.jp/dp/4297152754/">
    <img src="./image/amazon.png" class="mx-auto" alt="Claude Codeのシェア" />
    </a>
  </div>
<div>

---

# Claude Code のシェア
## やや他のツールに押され気味だが依然としてシェア1位

<div class="columns h-100">
  <div>
    <img src="./image/share-prev.png" alt="Claude Codeのシェア" />
  </div>
  <div>
    <img src="./image/share-current.png" alt="Claude Codeのシェア" />
  </div>
</div>

---

# 前提

- Claude Code のインターフェースや基本操作については割愛します。
- これ聞けば最新のアップデート含め「大体抑えるべきことわかった」を目指します。
- ただしClaude Codeの能力や活用方法は日々進化していますので現時点での試案的なものも含みます。


---

# 著作の紹介

12月5日刊行予定　日本で初めてのClaude Code刊行本<br>
「Claude CodeによるAI駆動開発入門」
現時点での教科書になることを目指しました。
<div class="columns">
  <div class="text-[28px]">
1章Claude Code入門と開発環境構築<br>
2章Claude CodeによるAI駆動開発の基礎<br>
3章MCPを活用したAIチャットボット開発<br>
4章並行処理とサブエージェントを使った開発手法<br>
5章セキュリティと応用的な活用
</div>
<div>
<a target="_blank" href="https://www.amazon.co.jp/dp/4297152754/">
  <img src="./image/book.png" alt="Claude Codeの本" style="height:50vh"/>
</a>
</div>
<div>


---

# 本日の御品書き

1. 最近のアップデートキャッチアップ(Agent Skills, Haiku4.5 、Opus4.5、Claude Code on the Web )
    - AgentSkills ハンズオン
    - Claude Code on the Web ハンズオン
2. あまり意識に上らないけど使っておくべき機能
4. ３つのコーディングエージェントの違い
3. プロジェクトの大きさによるClaude Codeの操縦方法
  特に大きなプロジェクトのために・・・
    - コンテキストウィンドウを知る。それを純粋に保つ
    - コードといかに向き合うか
4. 質疑応答

---

# この講演のゴールと効果

本書執筆にあたってドキュメントや公式Git、ブログを（恐らく）隅々まで読んだ自分として、「これはまず抑えておこう」「これは知っておくと業務で便利」という情報と実践知を共有。

何となく使ってた方も、この1時間弱で1段階段を上がれることを目的としたお話しとなります。

#### 持って帰って欲しいもの

Agent Skills, Claude Code on the web, （コンテキストウィンドウの理解）

---

# 最近のアップデートについて

基本はAgent SkillsはマストKnow

### **Agent Skills**
手順とプロンプトをClaude Codeに与えることができる。特定のタスクを実行するための小さなモジュール（スキル）を作成し、必要なタイミングで自動的に呼び出すことができる。
**⇨ LLMの柔軟性と推論力、コードの実行力、省コンテキスト占有とメリット大**

----


### **Haiku4.5**

Sonnet4.5で十分制限いっぱい動くMAXプランでは旨みは薄い。
従量課金でコストを下げたい方や制限のキツイProプランの方向け。Haikuで思考拡張モード（Ultrathink）で実行できるのもメリット。

１週間程度Haiku4.5だけで仕事してみたが、以前のHaikuと比べたら別物のように賢く、比較的違和感なく動くことも多い。(はっきり言って設定したのを忘れてた)
間違いやすいものとして、特にインフラタスクやエラー対応で中々解決できない時がある印象。

**ワンショットでTODOリストを作ってみた**

```
> TODOリストのアプリケーションを作ってください。
```

  <a target="_blank" href="https://client-bi979qxxr-sutefu23s-projects.vercel.app/">https://client-bi979qxxr-sutefu23s-projects.vercel.app/</a>

このクオリティなら十分満足

---


### **Opus4.5**

MAXプランおよびAPI課金で利用可能。

API課金でも以前の4.1の3分の1の価格。早い。MAXプランだとデフォルトで選択。

**こちらもワンショットでTODOリストを作ってみた**

<a target="_blank" href="https://todo-app-six-lilac-86.vercel.app/">https://todo-app-six-lilac-86.vercel.app/</a>

たまたまかもしれないが、ややリッチで高度ではある。

---

## API料金まとめ

| モデル|	入力 (Input) |出力 (Output) |
| :---: | :---: | :---: |
| Opus 4.5 |	$5.00 / 100万トークン |	$25.00 / 100万トークン |
| Opus 4.1 |	$15.00 / 100万トークン|	$75.00 / 100万トークン |
| Sonnet 4.5 |	$3.00 / 100万トークン|	$15.00 / 100万トークン |
| Haiku 4.5 |	$1.00 / 100万トークン|	$5.00 / 100万トークン |


---

# Agent Skills

### 概要

Claude Codeの最新機能。特定のタスクを実行するための小さな指示書（スキル）を作成し、必要に応じて自動的に呼び出すことができる。
MCPの問題点から、コンテキストの占有を最小限に抑える設計。(name, discriptionのみ。100トークン以下)

### 設定方法
`~/.claude/skills/`配下にMDファイルを保存することで利用可能。もしくはClaude自身に作ってもらえる。


---
<style scoped>
code{
  font-size:20px;
}
</style>

### スキル構成例

定義だけではなく、より具体的な例や参考ドキュメント、実行スクリプト、出力テンプレートなども含めることができる。

```
my-skill/
├── SKILL.md (必須)
├── reference.md (オプション：コンテキストに含めたいドキュメント)
├── examples.md (オプション：具体的な例)
├── scripts/
│   └── helper.py (オプション：実行するスクリプト)
└── templates/
    └── template.txt (オプション：出力テンプレートなど)
```

### 作り方 Claude Code自身に作ってもらう
```
> 新しいスキルを作ってください。
Claude Codeのエージェントがファイルを編集し終わった後、
その編集したファイルに対してLinterを実行するスキルです。
```

---


### 使用例

特定のタスク（例：コードレビュー、テストコード生成、ドキュメント生成など）を実行するためのモジュールとして使用。

**確定的な動作を行わせられる、LLMに柔軟なかつ例に沿った指示を与えられる、コンテキストを（ほとんど）占有しない。
基本的にはやりたいことは第一選択としてSkillsで実装するのがベスト。**

カスタムスラッシュコマンドで呼び出したり、サブエージェントのプロンプトに含めることが可能。

---

### Skillsのメリット

- **コンテキストの最小化**: 未使用時は最低限の情報のみを提供し、無駄なコンテキスト占有を防止
- **再利用性**: 一度作成したスキルを他のプロジェクトでも利用可能
- **柔軟性**: スクリプトやテンプレートを組み合わせて複雑なタスクも実行可能。出力形式も柔軟に指定可能
- **メンテナンス性**: スキル単位での更新や改善が容易
- **拡張性**: サブエージェントから呼び出したりカスタムスラッシュコマンドから呼び出すことが可能

---

## Skills 一緒に動かしてみましょう

```
> 適当なTypeScriptの関数を.tsファイルに書いて欲しいです。
例えば数字を引数に受け取ってその数字に3がつくか、
もしくは3の倍数の時はアホになる関数を出力してください。 
```

※動かない時のコツ

CLAUDE.mdに追記
```
## コード作成後の必須事項
  - TypeScript/JavaScriptファイルを作成・編集した後は、必ず `lint-checker` スキルを実行すること
```

---
<style scoped>
section{
  font-size:27px;
}
</style>

# Claude Code on the Web

[https://claude.ai/code](https://claude.ai/code)にアクセス

GitHubリポジトリを紐づけたら開始可能。

2.0.45より`&`をつけてプロンプトを送るとClaude Code on the Webにセッションを送れるようになった！

Claude Code GitHub Actionsとの違いとメリット
- セッションとして一つ付きのやり取りが可能
- 実行にあたっては独立したブランチと環境が用意される
- Hooksやサブエージェントが使える
- 非プログラマーでも扱いやすい
- サブスクユーザーのみ対象でAPIは含まない
- メインセッションからバックグラウンドタスクとしてセッションを送れる

---

### デメリット

- 開発サーバー起動（プレビューしながら開発）などはできない
- 立ち上げるたびにサンドボックス環境にて初期化されるため、使いこなそうと思うと`npm install`などの初期化コマンドはプロジェクトの`settings.json`のHookの`Session Start`として入れておくしかない。

### 画面

![height:300px](./image/claude-web.png)

---

## Claude Code on the web 一緒に動かしてみましょう

```
> & このアプリケーションの概要について説明してください。
```

---

# あまり意識に上らないけど使っておくべき機能

- /sandboxモード
- /output-style `Expranatory`

---

## **`/sandbox`モード**

OSレベルでのファイルシステムとネットワークの分離を行い、bashツールのファイルシステムアクセスを特定のディレクトリに制限することができる。<small class="inline">(MacとLinuxのみ。Windows未対応)</small>

Dockerでコンテナ化する必要が無く便利。

```setting.json
  "sandbox": {
    "enabled": true,
    "autoAllowBashIfSandboxed": true
  }
```
このように追記すれば、設定は永続化。（ただしユーザーディレクトリに入ってる情報、例えばGlobal管理されているキャッシュをクリアして問題解決、とかは難しくはなる。localhostなどにもアクセスできない）

やや不便さもあるので、Dockerの方が自由度は高い。


---

## **`/output-style`のExplanatory（説明的）**

1%しか使ってないマイナーな機能で一度非推奨マークされたが復活

AIで実装しているとどうしても、コード実装内容の解像度が落ち「具体的にどんな実装をしているか」「なぜそうしているか」に目がいかなくなりがち。

専門知識や「なぜそうしたのか」について「Insight」という技術的な解説と補足をつけて出力してくれるようになる。

![alt text](image/explanatory.png)

---

# ３つのコーディングツールの強みと違い

- **Claude Code**
優等生。バランスが良く、コーディングエージェントの様々な知見をいち早く盛り込む。基本間違いなし。
SkillやHook、スラッシュコマンド、サブエージェントなど、機能が多い。


- **Gemini CLI**
無料で使える範囲が大きい。
コンテキストウィンドウがデフォルトで大きい。

  仕様書理解やビジネス解像度が高い。本当に穴を理解している。
  コンテキストウィンドウが多いいからか、Figma MCPで再現が有利

---

- **Codex**
コード専用のLLMだから、コード理解がClaudeより優秀に感じることがある
Claudeと比べると遅い。2段階のプランしかない。


---

# ここからは設計の話になります。

---

# Claude Codeの違和感の正体

世の中で喧伝されて、実際に手元で爆速でコード生成する便利さと、それによって拡大した複雑さと複雑さのはざまで苦しみがある


---

# プロジェクトの大きさによってClaude Codeの活躍が変わる

 - 小規模なプロジェクトはワンショット、フューショットでも可能

 - しかし中規模・大規模なプロジェクトでは人間の目を離れたリスク、複雑化のリスクが無視できない。

---

# プロジェクトごとによるClaude Codeの操縦方法

注意: ここから先は主観的な内容も含まれます。

- 小規模プロジェクト
- 中大規模プロジェクト

---

## 下記レベルのアプリケーション開発ならVibeコーディングで可能になったのでは

- エンジニア一人で完結できるようなアプリケーション
- MVP開発やプロトタイピング
- 社内ツール用アプリケーション

---

# 小規模プロジェクトでのClaude Code

セッション間で共有できるのはCLAUDE.mdとコードが基本。
如何に実装プランとコンテキストを整理してClaude Codeに伝えるかが鍵。

これまで個人的にはPlanを立てて、Issueに分割し挙げてもらっていた。

Spec駆動開発で精度が高いものになった印象。

---

## **Spec駆動開発**

それぞれの段階フェーズに分け、次のステップに進む前に各ステップが適切に完了していることを保証

Kiro:
要件(requirements)⇒設計(design)⇒タスク(tasks)

Spec Kit:
仕様(specification)⇒計画(planning)⇒タスク作成(tasking)


「考慮漏れがあったので、作りなおし」という事が減る。特にSpec Kitの`clarify`フェーズが有効。

シングルショットでもかなりいける。

---

# 中規模以上で操作するClaude Code

前提として「コンテキストを理解する」「不要なコンテキストを混ぜない」

そして・・

- 如何に不確実性を下げるか
- LLMエージェントを如何に制御可能にするか
- 人間への可読性と理解をどう高めるか


---

# Context Windowを制する者はClaude Codeを制す
<a href="https://docs.claude.com/ja/docs/build-with-claude/context-windows" target="_blank">公式ドキュメント「コンテキストウィンドウ」</a>
![height:400px](./image/context-window-thinking.svg)
InputとOutputの両方を次のinputに含めて引き継いでいく。これがMAX20万トークン。
拡張思考の場合は会話のOutputに単発で含まれるが次に引き継がれない。

---

公式的にもコンテキストをいかに混ぜないか、という話

---

# Context Window が乱れるあるある

1. 実装をしていたら思ってもみないバグが出て解決のやり取りに時間が掛かった
2. 実装をしていたら内容について迷い始めて違うやり方でやり直し始めた
3. エラーメッセージが適切ではないものを送る。もしくは大量に関係ないものまで送る
4. IDE連携をしていてうっかり関係の無いファイルを開いて読ませてしまっている
5. CLAUDE.mdが更新されない古い情報やディレクトリ構成のまま
6. 余計なMCPサーバーのツール定義で、関係ない情報まで持っている

---

## 実装をしていたら思ってもみないバグが出て解決のやり取りに時間が掛かった

### 対策
`/conpact`...会話を要約している。引数に自然言語で指定したい内容を追加するか、CLAUDE.mdの`Summary instructions`の項目に設定を追加可能。

例：`実装の変更内容にフォーカスして要約してください。`


---

## 実装をしていたら内容について迷い始めて違うやり方でやり直し始めた

### 対策

`/rewind`...会話と変更ファイルをロールバック。Esc2回でも発動。
コンテキストウィンドウも戻るため、殆ど最強。

---

## エラーメッセージが適切ではないものを送る。もしくは大量に関係ないものまで送る

### 対策

エラー内容をちゃんと見る勇気。

<i>バグフィックスなどはサブエージェントに対応させればコンテキストは汚染されない。</i>

---

## IDE連携をしていてうっかり関係の無いファイルを開いて読ませてしまっている

### 対策

`/ide`で設定が元凶。
諸刃の剣。使っておくべき時もあるが玄人になってくると何をClaudeに渡しながらコーディングするかを頭の中で常に意識する必要がある

## 常に把握しておくべきもの
### CLAUDE.md、MCP、これまでの会話履歴、IDE連携


---

`/context`で見てみましょう。

```
    Context Usage
     ⛁ ⛁ ⛁ ⛁ ⛁ ⛁ ⛁ ⛀ ⛁ ⛁   claude-sonnet-4-5-20250929 · 82k/200k tokens (41%)
     ⛁ ⛁ ⛁ ⛁ ⛁ ⛁ ⛁ ⛁ ⛶ ⛶ 
     ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶   ⛁ System prompt: 2.4k tokens (1.2%)
     ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶   ⛁ System tools: 13.4k tokens (6.7%)
     ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶   ⛁ MCP tools: 15.0k tokens (7.5%)
     ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶   ⛁ Messages: 5.8k tokens (2.9%)
     ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶   ⛶ Free space: 118k (59.2%)
     ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛶ ⛝ ⛝ ⛝   ⛝ Autocompact buffer: 45.0k tokens (22.5%)
     ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ 
     ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ ⛝ 
```

MCPは結構食うので注意。
例えばGETしかしないのにPOSTのツール定義も読み込むため、MCPサーバーを全体に定義する時は注意。（最近問題視されてきている）

----

## CLAUDE.mdが更新されない古い構成のまま

- CLAUDE.mdの適切な分割。

  例：全体、フロントエンド、バックエンド、APIスキーマ、DBスキーマなど
  - front
  - api
  - scheme

- HooksやSkillsでファイルを作った時、セッション終了時などにプロンプトで命令しておくのは実行速度との相談だがアリだと思っている。（最近StopとSubagentStopのみプロンプトも書けるようになったが筆者が試したところ動かなかった）

あとはカスタムスラッシュコマンドで用意する、GitHub Actionsで更新する、などもあり。

---

## 余計なMCPサーバーのツール定義で、関係ない情報まで持っている

- Context7
- PlaywrightMCP

他にも...「サブエージェント」はコンテキストを占有する

特に~/.claudeの全体設定に入れるのは便利だが、不要なものも混じりやすいため、MCP、エージェントは気を付ける必要がある。
逆にHooks、Skills、カスタムスラッシュコマンドは常時占有するわけでは無い。

---

# コンテキストを意識できたら次はコードとどう向き合うか

- 如何に不確実性を下げるか
- LLMエージェントを如何に制御可能にするか
- 人間への可読性と理解をどう高めるか

---

## 原則1：如何に不確実性を下げるか。

<div class="columns">
  <div>
    <img src="./image/task-momentum.png" alt="中規模プロジェクトでのClaude Code" />
  </div>
  <div>
- 結果の不確実性<br/>
- 人間の手がどこまで入る必要があるかの判断<br/>
  </div>
</div>

---

## 原則2：LLMエージェントを如何に制御可能にするか

<div class="columns">
  <div>
    <img src="./image/abareuma.png" alt="中規模プロジェクトでのClaude Code" />
  </div>
  <div>
- Huskeyをまずインストールする<br/>
- `/sandbox`は設定しておく<br/>
- Linter、FormatterはHooksもしくはSkillsで設定<br/>
  </div>
</div>

---

## 原則3: 人間への可読性と理解をどう高めるか。

<div class="columns">
<div>

![height:400px](image/ai-human.png)

</div>
<div>
- `output-style`は`Explanation`にしておく<br/>
- CLAUDE.mdはセッション終了時に生成してもらう<br/>
</div>
</div>

---
<style scoped>
section {
  text-align: center;
}
h1{
  text-align: left;
}
</style>

# オニオンアーキテクチャの観点から考える

![height:500px center](./image/domain.png)

---

## **インフラ層はコンテキストが薄い**

- インフラ層のコードは標準化しやすい
外部APIの呼出し、DB接続、認証・認可、ログ管理、ストレージサービス(S3等)への保存など
組織としてたくさん作っておくと資産になる

---

## **ドメイン層はボイラープレート化しやすい**

⇒　ドメインオブジェクトとロジックの定義ファイルからスキル化しやすい。

<div class="columns">
<div>

##### ドメインオブジェクト
```
class User {
  constructor(id, name, email) {
    this.id = id;
    this.name = name;
    this.email = email;
  }
}
```

</div>
<div>

##### ドメインサービス
```
class UserService {
  constructor(userRepository) {
    this.userRepository = userRepository;
  }

  async createUser(userData) {
    // ユーザ作成のビジネスロジック
    return this.userRepository.save(userData);
  }

  async getUserById(userId) {
    // ユーザ取得のビジネスロジック
    return this.userRepository.findById(userId);
  }
}
```

</div>

</div>

---

## **その他の層（テスト・UI）**

**単体テスト、UI層のコンポーネントもSkills化しやすい。**

**組織でテスト、UIコンポーネントのベストプラクティスの型をいち早く作っておくべき。**

UIコンポーネントはFigmaMCPサーバーで8割9割自動化できる。

GeminiCLIの方がコンテキストが長大（100万トークン）のため、可能な範囲が広い。

Claude Sonnet4.5でも100万トークン対応可能だが、APIのみなのとコストが高い。


---

# まとめ

- 常にコンテキストウィンドウに何が入っているかを意識する
⇨ CLAUDE.md、MCP、これまでの会話、IDE連携
- 予測可能性、制御可能性を高める
⇨Husky, Linter, Formatter
- 可読性、理解性を高める
⇨ドメイン駆動設計などの設計原則が役立つと思っている。

---

# 最後に

- 気軽に連絡してください。 **<a target="_blank" href="https://x.com/t_hirakawa">@t_hirakawa</a>**
導入支援や講演のご依頼も歓迎します。⇨<a href="mailto:info@en-gine.co">メール</a>

- お仕事の相談も募集中

- AIxシステム開発の引き合いも増加中。
お仲間募集中なのでカジュアル面談しましょう。
PM、エンジニア、営業（業務委託や社員登用）

---

# 質疑応答

---
<style scoped>
section {
  text-align: center;
}
</style>

# 本もよろしくお願いします！<br><br>「Claude CodeによるAI駆動開発入門」

<a href="https://www.amazon.co.jp/dp/4297152754/" target="_blank"><img src="./image/book.png" alt="Claude CodeによるAI駆動開発入門" /></a>
