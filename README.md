# decision-review

SDDの要件・設計・実装でAIが下した判断のうち、人間に確認すべき重要なものを抽出する実験用Agent Skillです。

The same `SKILL.md` works in Cursor and Claude Code. It extracts decisions that need human review from requirements, design, and implementation changes.

## かんたんインストール

[Node.js](https://nodejs.org/) が入っていれば、ターミナルで次の1行を実行できます。CursorとClaude Codeの両方へ、全プロジェクトで使えるようにインストールします。

```sh
npx skills add usuiatsushi/decision-review -a cursor -a claude-code -g --copy -y
```

今開いているプロジェクトだけで使う場合は `-g` を外してください。片方だけなら不要な `-a cursor` または `-a claude-code` を外せます。導入後はAgentで `/decision-review` を指定します。

## 何をするか

- Intent、Spec、Design、変更差分から判断候補を洗い出す
- 目的の解釈、外部に見える振る舞い、安全性、変更しにくさ、既存仕様との矛盾、影響のある仮定を基準にエスカレーションする
- AIの推奨、根拠、代替案、影響範囲をDecision票にまとめる
- 人間の修正をAIが再レビューし、確定した判断を成果物に対応づける

初期版は小さな開発タスクで判定基準の見落としを検証するためのものです。成果物の差分確認、テスト、最終Acceptanceを省略しないでください。

## 手動インストール

このリポジトリ内の `decision-review` フォルダをコピーします。1つのプロジェクトで両方使うなら次の配置で共有できます。

```text
プロジェクト/.claude/skills/decision-review/SKILL.md
```

Cursor専用のプロジェクト配置は `.cursor/skills/decision-review/SKILL.md`、個人用はCursorが `~/.cursor/skills/decision-review/SKILL.md`、Claude Codeが `~/.claude/skills/decision-review/SKILL.md` です。

## 使い方

Agentに `/decision-review` を指定し、Intent、制約、既存Spec・Design、今回の差分を渡します。例：

> /decision-review 今回の要件Spec変更から、人間が判断すべきDecisionを抽出して。根拠と代替案も示して。

まずDecision票を見て判断し、次に差分を確認して、票に載らなかった重要判断を記録します。

## ライセンス

MIT License。詳しくは [LICENSE](LICENSE) を参照してください。
