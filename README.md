# BatchRenamer

Unity Editor 専用の **一括リネームツール** です。  
シーン内の GameObject や Project 内のアセット名を、置換・削除・接頭辞/接尾辞追加・連番フォーマットなどでまとめて変更できます。  
プレビュー → 実行 → Undo（GameObject）に対応します。

---

### ✨ 主な機能

#### 基本
- **対象範囲の選択**  
  - Selection（選択中オブジェクト/アセット）  
  - Active Scene（現在シーン内の全 GameObject）  
  - Project Assets（全アセット or 選択アセットのみ）
- **リネームモード**  
  - Replace/Remove（指定ワードを置換・削除）  
  - Add Prefix/Suffix（接頭辞・接尾辞追加）  
  - Format（`{name}`/`{counter}`/`{date}`/`{guid}` などテンプレート式）
- **連番オプション**  
  開始値 / 桁数 / ステップ / 重複回避（自動ユニーク化）
- **プレビュー機能**  
  実行前に「変更前 / 変更後」を一覧で確認可能

#### 拡張
- **正規表現 / 大文字小文字区別 / 単語一致** に対応  
- **アセット名の重複チェック** → 自動で `_1` `_2` … を付与して回避  
- **Undo**  
  - GameObject 名変更は Undo に対応  
  - アセット名変更は `AssetDatabase.RenameAsset` による直接変更（Undo 非対応）

---

### 📂 フォルダ構成

    Assets/
    └─ IGNORANZ PROJECT/
       └─ BatchRenamer/
          └─ BatchRenamerWindow.cs   // メインUI（EditorWindow）

---

### 🚀 使い方

#### 基本操作
1. Unity メニューから **Tools > Batch Renamer** を選択  
2. 対象範囲とモードを選択  
3. **Preview** で結果を確認  
4. 問題なければ **Apply** でリネーム実行

#### 例
- 「(Clone)」をすべて削除  
  - Mode: ReplaceRemove / Find=`(Clone)` / Replace=`(空)`
- すべてに `UI_` を付ける  
  - Mode: AddPrefixSuffix / Prefix=`UI_`
- `Enemy_001, Enemy_002, …` のように連番  
  - Mode: Format / Template=`Enemy_{counter:000}` / Start=1, Pad=3

---

### 📝 出力例（Preview）

    Type       Original          Proposed        Status
    GameObject Enemy(Clone)      Enemy           OK
    GameObject Enemy(Clone)(1)   Enemy_1         OK
    Asset      MyScript_old.cs   MyScript.cs     OK

---

### ⚙️ 注意事項
- **アセット名変更**は Undo 非対応 → 実行前に VCS / バックアップ推奨  
- **GameObject 名変更**は Undo 対応（Ctrl+Z で戻せます）  
- 無効文字（`/ : * ? " < > |` 等）は自動でエラー表示  
- 大量のアセットを対象にする場合、Project 全体検索は時間がかかります

---

### 📜 ライセンス

MIT License  
（ただし大規模な一括編集の際にはバックアップを作成してください）
