# whistle-piano

実機写真レイアウト（白14 / 黒10 / 合計24鍵）向けの「口笛鍵盤ナビ」Webアプリです。  
`index.html` 1ファイルに HTML/CSS/JavaScript を内包し、GitHub Pages で公開できます。

## 機能

- 口笛のリアルタイム音程推定（300Hz〜2500Hz）
- 3点固定校正（Key 1 / Key 13 / Key 24）
- 校正式: `p = log2(freq)`, `p_corrected = α * p + β`（最小二乗）
- 補正済み全鍵テーブル（24鍵）を生成し、通常運転はそのテーブルのみ使用
- Key IDは左→右の物理順（白黒共通連番）
- Key番号主表示 + ドレミ任意編集
- 安定化（EMA平滑化 + 6フレーム連続確定 + 直前Key保持）
- メロディ記録（安定Key + 休符）と再生ナビ
- 設定（感度 低/中/高、デバッグ表示）
- 校正JSONのエクスポート / インポート / 削除
- 保存先: IndexedDB（失敗時 localStorage）
- 初回読み込み後のオフライン利用（Service Worker + Cache）

## GitHub Pages公開方法

1. `whistle-piano` の内容を GitHub リポジトリへ push
2. GitHub の `Settings` → `Pages` を開く
3. `Build and deployment` の `Source` を `Deploy from a branch` に設定
4. ブランチ（例: `main`）とフォルダ（`/ (root)`）を選択して保存
5. 数分待って公開URLへアクセス

## 使い方（校正 → 演奏 → 記録）

1. `マイク開始` を押す
2. `校正を開く` → `3点校正 (Key 1 / Key 13 / Key 24)`
3. 指示された3鍵を順に鳴らす（各2.0秒、末尾1.0秒中央値）
4. 校正完了後、口笛を吹いて鍵盤ナビを確認
5. `記録開始` で履歴を作り、`再生ナビ` で順次ハイライト再生

## 校正JSON仕様

```json
{
  "instrument": "KAWAI_toy_piano_photo_layout_24",
  "calibration_mode": "three_point_fixed",
  "key_id_rule": "left_to_right_physical_order",
  "base_key_ids": [1, 13, 24],
  "alpha": 1.0,
  "beta": 0.0,
  "anchors": [
    {"id":1,"label":"ド","measured_freq_hz":261.3,"reference_freq_hz":261.625565}
  ],
  "created_at": "ISO8601",
  "keys": [
    {"id":1,"label":"ド","freq_hz":261.3}
  ]
}
```

## 受け入れ条件チェックリスト

`ACCEPTANCE_CHECKLIST.md` を参照してください。
