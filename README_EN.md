# BatchRenamer

A Unity Editor–exclusive **batch renaming tool**.
It allows you to rename GameObjects in the Scene and assets in the Project all at once, supporting replace/remove, prefix/suffix addition, and sequential numbering formats.
Supports Preview → Apply → Undo (for GameObjects).

---

### ✨ Features

#### Basic
- **Target Scope**
  - Selection (selected GameObjects/assets)
  - Active Scene (all GameObjects in the current scene)
  - Project Assets (all assets or only selected ones)
- **Rename Modes**
  - Replace/Remove (replace or delete specific words)
  - Add Prefix/Suffix (add text before or after names)
  - Format (template with `{name}` / `{counter}` / `{date}` / `{guid}`)
- **Counter Options**
  Start value / Padding digits / Step / Conflict auto-resolution
- **Preview**
  Check all name changes before applying

#### Extended
- Supports **Regex / Case Sensitivity / Whole Word** options
- **Duplicate name check** for assets → auto `_1`, `_2`, … suffixes
- **Undo**
  - GameObject renames support Undo
  - Asset renames use `AssetDatabase.RenameAsset` (Undo not supported)

---

### 📂 Folder Structure

    Assets/
    └─ IGNORANZ PROJECT/
       └─ BatchRenamer/
          └─ BatchRenamerWindow.cs   // Main UI (EditorWindow)

---

### 🚀 Usage

#### Basic Steps
1. Open **Tools > Batch Renamer** from the Unity menu
2. Select target scope and rename mode
3. Click **Preview** to see results
4. If correct, click **Apply** to rename

#### Examples
- Remove all “(Clone)” suffixes
  - Mode: ReplaceRemove / Find=`(Clone)` / Replace=`(empty)`
- Add `UI_` prefix to all names
  - Mode: AddPrefixSuffix / Prefix=`UI_`
- Generate sequential names: `Enemy_001, Enemy_002, …`
  - Mode: Format / Template=`Enemy_{counter:000}` / Start=1, Pad=3

---

### 📝 Preview Example

    Type       Original          Proposed        Status
    GameObject Enemy(Clone)      Enemy           OK
    GameObject Enemy(Clone)(1)   Enemy_1         OK
    Asset      MyScript_old.cs   MyScript.cs     OK

---

### ⚙️ Notes
- **Asset renames** do not support Undo → use VCS/backup before applying
- **GameObject renames** support Undo (Ctrl+Z)
- Invalid characters (`/ : * ? " < > |` etc.) are automatically flagged
- Renaming large amounts of assets may take time when scanning the entire Project

---

### 📜 License

MIT License
(We recommend creating backups when performing large-scale renaming.)