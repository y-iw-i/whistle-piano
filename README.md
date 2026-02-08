# whistle-piano

21鍵おもちゃピアノ向けの「口笛鍵盤ナビ」Webアプリです。  
`index.html` 1ファイルに HTML/CSS/JavaScript を内包し、GitHub Pages で公開できます。

## 機能

- 口笛のリアルタイム音程推定（300Hz〜2500Hz）
- 21鍵フル校正（2.0秒計測、最後1.0秒中央値）
- 校正値ベースの鍵盤ナビ（Key ID + ドレミ）
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
2. `校正を開く` → `全21鍵を校正`
3. 表示された `Key X（ドレミ）` を順番に鳴らす
4. 校正完了後、口笛を吹いて鍵盤ナビを確認
5. `記録開始` で履歴を作り、`再生ナビ` で順次ハイライト再生

## 校正JSON仕様

```json
{
  "instrument": "KAWAI_toy_piano_21",
  "created_at": "ISO8601",
  "keys": [
    {"id":1,"label":"ド","freq_hz":261.3}
  ]
}
```

## 受け入れ条件チェックリスト

`ACCEPTANCE_CHECKLIST.md` を参照してください。
