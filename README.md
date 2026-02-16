# Personal Skill Dashboard (Jekyll)

このリポジトリは、Excelスキルシートを元にした「個人用スキルダッシュボード + スキル台帳 + 実績(Evidence)」を GitHub Pages(Jekyll) で管理するための構成です。

## 追加したページ

- `/dashboard/` : 強みTop5 / 弱みTop5 / 次アクションTop10
- `/skills/` : スキル台帳（カテゴリ別 + フィルタ）
- `/evidence/` : 実績一覧
- `/evidence/*` : 個別Evidenceページ

## データファイル

- `_data/skills.yml`
- `_data/goals.yml`
- `_data/evidence.yml`

## 入力データの扱い

- 優先入力: `/mnt/data/スキルシート_K.N_茂原_260213.xlsx`
- フォールバック: `/Users/namil/Downloads/スキルシート_K.N_茂原_260213.xlsx`

## スキル推定ルール

### 1) 評価記号 → base_level

- `★ = 4`
- `〇 = 3`
- `△ = 2`
- 空欄 = `1`

### 2) level(0-5)

- `level = min(5, base_level + recency_bonus + multi_project_bonus)`
- `recency_bonus = 1` if `last_used >= 2025-01`, else `0`
- `multi_project_bonus = 1` if `evidence` が2件以上, else `0`

### 3) confidence(A/B/C)

- `A`: `level >= 4` かつ `evidence >= 1`
- `B`: `level == 3` または stale高め
- `C`: `level <= 2` または根拠が弱い

### 4) stale_score（基準日: 2026-02）

- `0-3ヶ月: 0`
- `4-6ヶ月: 1`
- `7-12ヶ月: 2`
- `13-24ヶ月: 3`
- `25-36ヶ月: 4`
- `37ヶ月以上: 5`

### 5) 次アクション優先度

- `gap = max(target.m3 - level, 0)`
- `no_evidence = 1` if evidence 空, else `0`
- `low_confidence = 1` if confidence is `B` or `C`, else `0`
- `priority_score = gap*3 + stale_score*2 + no_evidence*2 + low_confidence*1`

### 6) 強みスコア（Dashboard表示用）

- `strength_score = level*4 + evidence_count*2 + confidence_bonus - stale_score`
- `confidence_bonus`: `A=2`, `B=1`, `C=0`

## 更新運用

1. Excelから案件経歴と技術経験記号を更新
2. `_data/skills.yml` の `last_used / evidence / target / next_action` を更新
3. 必要に応じて `evidence/*.md` を追加し `_data/evidence.yml` に登録
4. ローカル検証

```bash
bundle exec jekyll build --destination /tmp/namil-jekyll-build
```

## 注意

- スキルの「できる」は Evidence と紐づける
- 根拠が弱いスキルには必ず `next_action` を設定する
- 既存ページ（プロフィール等）は今回の最小追加方針で未変更
