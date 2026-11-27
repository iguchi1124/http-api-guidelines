# HTTP API Guidelines — Agent Skills

HTTP APIの設計・実装・レビューに適用する、[Agent Skills形式](https://agentskills.io/specification)の共通配布物。規約本文は[HTTP API開発ガイドライン](skills/http-api-guidelines/references/http-api-guidelines.md)を参照する。

本体は`skills/http-api-guidelines/`にある。標準のSKILL.mdと相対参照のドキュメントで構成し、対応するエージェントへフォルダー単位で配置できる。Claude Codeからも通常のスキルとして利用できる。

## 構成

```text
http-api-guidelines/
├── AGENTS.md
├── CLAUDE.md
├── README.md
└── skills/http-api-guidelines/
    ├── SKILL.md
    └── references/http-api-guidelines.md
```

- `SKILL.md`: スキルの名前・説明・適用手順。
- `references/http-api-guidelines.md`: 規約本文の唯一の編集元。
- ルートの`AGENTS.md`と`CLAUDE.md`: このリポジトリを直接扱うエージェント向けの入口。スキル単体の利用には不要。

特定ホスト用のプラグインマニフェスト、MCPサーバー、実行スクリプトは不要。Agent Skillsはスキルの形式を規定するものであり、自動検出する配置先やインストール手順は各ホストに従う。

## 取得

任意の作業ディレクトリで実行する。

```sh
git clone https://github.com/iguchi1124/http-api-guidelines.git
```

利用するエージェントが指定するスキル配置先に、`skills/http-api-guidelines/`をフォルダーごと配置する。SKILL.mdに加えてreferencesも含める。

## Claude Codeでスキルとして利用する

Claude CodeはAgent Skills形式を扱い、プロジェクト用は`.claude/skills/`、個人用は`~/.claude/skills/`からスキルを読み込む。[Claude Code公式スキルガイド](https://code.claude.com/docs/en/skills#where-skills-live)

初回配置の例。対象プロジェクトのルートで実行し、`/absolute/path/to/http-api-guidelines`をclone先の絶対パスに置き換える。

```sh
mkdir -p .claude/skills
cp -R /absolute/path/to/http-api-guidelines/skills/http-api-guidelines .claude/skills/
```

配置後は次の構造になる。

```text
.claude/skills/http-api-guidelines/
├── SKILL.md
└── references/http-api-guidelines.md
```

対象プロジェクトでClaude Codeを起動し、次のように呼び出す。

```text
/http-api-guidelines 注文キャンセルAPIの設計を確認して
```

説明に合致する依頼では自動選択の対象にもなる。個人用として使う場合は、同じフォルダーを`~/.claude/skills/http-api-guidelines/`へ配置する。同名のスキルがすでにある場合は、既存の変更を確認してから更新する。[スキルの呼び出し](https://code.claude.com/docs/en/skills)

## Claude CodeからMarkdownとして参照する

スキル登録を使わない場合は、配布フォルダー全体を対象プロジェクトの`docs/http-api-guidelines/`へ配置し、プロジェクトルートのCLAUDE.mdに次を追記する。

```text
@docs/http-api-guidelines/skills/http-api-guidelines/references/http-api-guidelines.md
```

既存のAGENTS.mdには同じファイルを読み、HTTP API作業に適用する指示を追記する。既存ファイル全体を上書きしない。

CLAUDE.mdの`@`による相対参照は、そのCLAUDE.mdを基準に解決される。スキルが使用時に読み込まれるのに対し、この方法では規約をプロジェクトのコンテキストとして読み込む。[Claude Code公式メモリーガイド](https://code.claude.com/docs/en/memory#import-additional-files)

## 更新と移行

- 配布元の変更は`git pull --ff-only`で取得し、配置したスキルへ必要な差分を反映する。コピー配置は自動更新されない。
- 規約本文はreferences内の1か所で管理する。
- 共有ルールや参照先を変えるときは、AGENTS.mdとCLAUDE.mdを整合させる。
- 旧版をClaudeプラグインとして使っていた場合は、その読み込み設定を外し、上記の通常スキル配置へ移行する。呼び出し名は`/http-api-guidelines`になる。

規約本文の採用方針（snake_case、Problem Detailsなど）はこの配布形式の変更でも維持する。

## 検証範囲

Agent Skills形式、スキルの単体コピー後の相対参照、CLAUDE.mdの参照先、AGENTS.mdとの共有ルール、JSON例を検証する。実際のモデルによるスキル選択・呼び出しは未検証。

このリポジトリの取得だけでは、他プロジェクトやユーザー全体の設定には登録されない。
