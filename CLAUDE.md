# pokemon-type-matrix

Pokémon GO PvP のタイプ相性表ツール（単一HTML `type-matrix.html`。GOの×1.6計算式で攻撃×防御の倍率を表示。18の単タイプ＋任意の複合タイプ、レギュレーション絞り込み、攻撃列の固定スクロールに対応）。

## 収録物

| ファイル | 中身 |
|---|---|
| `type-matrix.html` | タイプ相性表ツール（引く用） |
| `quiz.html` | タイプ相性クイズ 60秒（覚える用／提案P-013の1本目） |

### quiz.html について

**誰がどの瞬間に触るか**：Pokémon GO PvP をやる人が、対戦前や移動中に「表を見ずに倍率を反射で出せるか」を試したくなった瞬間。

- 相性表ツールと **`TYPE_CHART` / `TYPES` を同一データで持つ**（3,078通り＝18攻撃×(18単+153複合)を機械検証済み。倍率は全て選択肢バケットでカバー）
- 60秒・4択・5連続ごとに加点・自己ベストは localStorage
- 単タイプ／複合ありの2モード、結果の共有テキスト生成
- **相性表を更新したら quiz.html 側の TYPE_CHART も同じ値に揃えること**（2箇所に同じ表がある。ズレたら検証スクリプトで気づけるようにするのが次の改善案）

## アクセス計測（2026-08-11 設置）

`quiz.html` の `<head>` に GoatCounter のスニペットがある。**`window.GC_CODE` が `"MYCODE"` の
間は外部スクリプトを一切読み込まない**（＝計測は動かない・通信もしない）。実コードに書き換えると動き出す。

- 同じスニペットが `diet-pace-simulator/index.html` にもある。**片方を直したらもう片方も揃える**
- 2作品とも `takakun-art.github.io` 配下なので、GoatCounterのサイト登録は**1つでよい**（パスで区別）
- 送っているイベント: `quiz-start-single` / `quiz-start-dual` / `quiz-complete` / `quiz-share`
- **スコア・回答内容は送らない。** 送るのは「開始した・完走した・共有した」という事実だけ
- 計測が壊れてもクイズ本体は動く（`gcEvent` は未ロード時に黙って捨てる）
- 記録と週次報告は `~/.claude/scheduled-tasks/product-traffic-weekly/SKILL.md` が担当

## 運用ルール
- Git運用は `~/.claude/CLAUDE.md` の「Git 運用ルール」に従う（ファイルを作成・更新したら必ずコミット。コミット本文に判断者〈くんたか / Claude〉と変更理由を書く）。
