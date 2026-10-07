# C100297422 Manifest Difference

Comparison of TFS pending-change manifests.

| File | Role |
|---|---|
| `C100297422-manifestA.txt` | Original shelveset on `$/DCS/DEV-UPGRADE` |
| `C100297422-manifestB.txt` | Re-shelve on `$/DCS/DEV-UPGRADE-DUTYSTAMP` |

Paths below drop the branch prefix (`$/DCS/DEV-UPGRADE/` vs `$/DCS/DEV-UPGRADE-DUTYSTAMP/`) so the same relative file can be compared.

TFS labels from the source manifests are written in English here (`add` / `edit` / `delete`, ISO dates) so this file stays UTF-8 and renders cleanly on GitHub.

---

## 1. Header / metadata

| Field | Manifest A | Manifest B |
|---|---|---|
| TFS branch | `$/DCS/DEV-UPGRADE` | `$/DCS/DEV-UPGRADE-DUTYSTAMP` |
| Shelveset | `C100297422 DSS & JQuery v0.9` | `C100297422 DSS & JQuery v0.9 New Branch` |
| User | `victor_yt_lam` | `victor_yt_lam` |
| Lock | none (all entries) | none (all entries) |
| Date | all `2026-09-17 15:52:42` | `2026-10-07` 11:16-11:45 (see section 1.1) |
| Total entries | **465** | **433** |
| Unique relative paths | 465 (no duplicates) | 433 (no duplicates) |

### 1.1 Date breakdown (B only)

A uses one timestamp for every entry. B uses several timestamps from the same morning:

| Timestamp (B) | Count | Typical meaning |
|---|---:|---|
| 2026-10-07 11:16:09 | 39 | early unshelve / edits |
| 2026-10-07 11:16:10 | 1 | |
| 2026-10-07 11:16:13 | 16 | |
| 2026-10-07 11:16:14 | 1 | |
| 2026-10-07 11:16:17 | 4 | |
| 2026-10-07 11:16:18 | 5 | |
| 2026-10-07 11:16:20 | 19 | |
| 2026-10-07 11:16:22 | 20 | |
| 2026-10-07 11:16:23 | 5 | |
| 2026-10-07 11:16:24 | 1 | |
| 2026-10-07 11:16:26 | 8 | |
| 2026-10-07 11:17:27 | 256 | adds |
| 2026-10-07 11:17:28 | 57 | deletes |
| 2026-10-07 11:45:48 | 1 | `Web.config` only (not in A) |

---

## 2. Change-type counts

| Change | A | B | Delta (B minus A) |
|---|---:|---:|---:|
| add | 271 | 256 | -15 |
| edit | 137 | 120 | -17 |
| delete | 57 | 57 | 0 |
| **Total** | **465** | **433** | **-32** |

| File type | A | B | Delta (B minus A) |
|---|---:|---:|---:|
| big5 | 200 | 200 | 0 |
| utf-8 | 188 | 184 | -4 |
| Binary | 63 | 49 | -14 |
| (empty - folder add) | 14 | 0 | -14 |

The file-type deltas come only from the A-only entries in section 4. Shared paths have the same file type.

---

## 3. Path overlap (relative path)

| Set | Count |
|---|---:|
| In both A and B | **432** |
| Only in A | **33** |
| Only in B | **1** |

For the 432 shared paths:

- Change type is **identical** (no add / edit / delete mismatch).
- File type is **identical**.
- Shared breakdown: **256 add**, **119 edit**, **57 delete**.

What still differs on those 432 paths: branch prefix, shelveset name, date, and base changeset (see section 6).

---

## 4. Only in A (33) -- not on the new branch

These relative paths appear in `manifestA.txt` and do **not** appear in `manifestB.txt`.

### 4.1 Application source edits (5) -- highest risk

| Change | Base ver | Type | Relative path |
|---|---|---|---|
| edit | C7749 | utf-8 | `DCS/DCS/Areas/CE/Controllers/FCE006Controller.cs` |
| edit | C7749 | utf-8 | `DCS/DCS/Areas/PP/AP/Controllers/FCA003Controller.cs` |
| edit | C7936 | utf-8 | `DCS/DCS/Areas/PP/AP/Models/Dao/APEnqDao.cs` |
| edit | C7918 | utf-8 | `DCS/DCS/Areas/PP/EP/Models/Dao/EPEnqDao.cs` |
| edit | C7749 | utf-8 | `DCS/DCS/Areas/PP/PE/Scripts/FPE024S01.js` |

These A-only source edits were not re-shelved onto `DEV-UPGRADE-DUTYSTAMP`. Confirm whether the DUTYSTAMP tip already contains the change, or whether they still need to be applied.

### 4.2 Deployed jQuery UI theme images (13)

All **edit**, base `C7749`, type `Binary`, under `DCS/DCS/Content/themes/base/images/`.

B does **not** edit these deployed copies. B still **adds** the same filenames under the NuGet package path `DCS/packages/jQuery.UI.Combined.1.14.1/Content/Content/themes/base/images/` (those package adds are in both manifests).

| File |
|---|
| `ui-bg_flat_0_aaaaaa_40x100.png` |
| `ui-bg_flat_75_ffffff_40x100.png` |
| `ui-bg_glass_55_fbf9ee_1x400.png` |
| `ui-bg_glass_65_ffffff_1x400.png` |
| `ui-bg_glass_75_dadada_1x400.png` |
| `ui-bg_glass_75_e6e6e6_1x400.png` |
| `ui-bg_glass_95_fef1ec_1x400.png` |
| `ui-bg_highlight-soft_75_cccccc_1x100.png` |
| `ui-icons_222222_256x240.png` |
| `ui-icons_2e83ff_256x240.png` |
| `ui-icons_454545_256x240.png` |
| `ui-icons_888888_256x240.png` |
| `ui-icons_cd0a0a_256x240.png` |

Full relative path prefix: `DCS/DCS/Content/themes/base/images/`

### 4.3 Binary add (1)

| Change | Base ver | Type | Relative path |
|---|---|---|---|
| add | - | Binary | `DCS/DCS/Ref/CommonCipher.dll` |

### 4.4 Package folder adds (14)

All **add**, no base version, empty file type (TFS folder pending-add). The **files** under these folders are already in both manifests; only the folder nodes themselves are missing from B.

| Relative path |
|---|
| `DCS/packages/Microsoft.jQuery.Unobtrusive.Validation.4.0.0` |
| `DCS/packages/Microsoft.jQuery.Unobtrusive.Validation.4.0.0/Content/Scripts` |
| `DCS/packages/fullcalendar.3.9.0` |
| `DCS/packages/fullcalendar.3.9.0/content/Content` |
| `DCS/packages/fullcalendar.3.9.0/content/Scripts/fullcalendar` |
| `DCS/packages/fullcalendar.3.9.0/content/Scripts/fullcalendar/locale` |
| `DCS/packages/jQuery.3.7.1` |
| `DCS/packages/jQuery.3.7.1/Content/Scripts` |
| `DCS/packages/jQuery.3.7.1/Tools` |
| `DCS/packages/jQuery.UI.Combined.1.14.1` |
| `DCS/packages/jQuery.UI.Combined.1.14.1/Content/Content/themes/base` |
| `DCS/packages/jQuery.UI.Combined.1.14.1/Content/Content/themes/base/images` |
| `DCS/packages/jQuery.UI.Combined.1.14.1/Content/Scripts` |
| `DCS/packages/jQuery.UI.Combined.1.14.1/Tools` |

---

## 5. Only in B (1) -- new on DUTYSTAMP

| Change | Base ver | Type | Date | Relative path |
|---|---|---|---|---|
| edit | C7950 | utf-8 | 2026-10-07 11:45:48 | `DCS/DCS/Web.config` |

This is the latest timestamp in B and does not exist in A. It looks like a branch-specific config edit after the unshelve, not part of the original 2026-09-17 shelveset.

TFS path in B:

```
$/DCS/DEV-UPGRADE-DUTYSTAMP/DCS/DCS/Web.config;C7950
```

---

## 6. Shared paths (432) -- metadata-only differences

Relative path and change type match. These fields differ on every shared entry:

| Field | A | B |
|---|---|---|
| Server path prefix | `$/DCS/DEV-UPGRADE/` | `$/DCS/DEV-UPGRADE-DUTYSTAMP/` |
| Shelveset | `C100297422 DSS & JQuery v0.9` | `C100297422 DSS & JQuery v0.9 New Branch` |
| Date | 2026-09-17 15:52:42 | 2026-10-07 (various) |
| Base changeset on edit/delete | mixed (`C7749`, `C7935`, ...) | **all `C7950`** |
| Base changeset on add | none | none |

### 6.1 Base changeset remapping (shared paths)

| Count | A version | B version | Typical change |
|---:|---|---|---|
| 256 | - (no version) | - (no version) | add |
| 132 | C7749 | C7950 | edit / delete |
| 13 | C7935 | C7950 | edit |
| 9 | C7865 | C7950 | edit |
| 5 | C7870 | C7950 | edit |
| 4 | C7922 | C7950 | edit |
| 2 | C7750 | C7950 | edit |
| 2 | C7886 | C7950 | edit |
| 2 | C7931 | C7950 | edit |
| 2 | C7761 | C7950 | edit |
| 2 | C7921 | C7950 | edit |
| 1 | C7862 | C7950 | edit |
| 1 | C7907 | C7950 | edit |
| 1 | C7799 | C7950 | edit |

A-only versions that never appear on a shared path (they belong to section 4.1): `C7936` (`APEnqDao.cs`), `C7918` (`EPEnqDao.cs`).

### 6.2 Shared edit files (119)

These source/config edits exist in **both** manifests (same relative path and edit). Listed so it is clear they are **not** missing from B.

**Project / shared**

- `DCS/DCS/DCS.csproj`
- `DCS/DCS/packages.config`
- `DCS/DCS/Views/Shared/_Layout.cshtml`
- `DCS/DCS.Models/DCS.Models.csproj`
- `DCS/DCS.Models/Entities/CD_COMM_VW.cs`
- `DCS/DCS.Models/Entities/CED94_HDR_VW.cs`
- `DCS/DCS.Models/Entities/DCSEntities.cs`
- `DCS/DCS.Utils/Constants/ConstantKeys.cs`
- `DCS/DCS.Utils.PermitProcessing/Ls_Approve.cs`
- `DCS/DCS.Utils.PermitProcessing/PermitCancelApplication.cs`
- `DCS/DCS.Utils.PermitProcessing/PermitRejection.cs`

**CE**

- `DCS/DCS/Areas/CE/Controllers/FCE001Controller.cs`
- `DCS/DCS/Areas/CE/Controllers/FCE003Controller.cs`
- `DCS/DCS/Areas/CE/Controllers/FCE004Controller.cs`
- `DCS/DCS/Areas/CE/Models/Dao/CEEnqDao.cs`
- `DCS/DCS/Areas/CE/Models/Dao/CEMaintDao.cs`
- `DCS/DCS/Areas/CE/Models/Model/FCE001/FCE001E01Model_new.cs`
- `DCS/DCS/Areas/CE/Models/Model/FCE003/FCE003D01_1Model.cs`
- `DCS/DCS/Areas/CE/Scripts/FCE001E01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE001E01_New.js`
- `DCS/DCS/Areas/CE/Scripts/FCE001S01_New.js`
- `DCS/DCS/Areas/CE/Scripts/FCE003D01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE003_FCE004Share.js`
- `DCS/DCS/Areas/CE/Scripts/FCE004E01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE008C01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE008S01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE009Base.js`
- `DCS/DCS/Areas/CE/Scripts/FCE009S01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE013S01.js`
- `DCS/DCS/Areas/CE/Scripts/FCE015S01.js`
- `DCS/DCS/Areas/CE/Utils/CEEnums.cs`
- `DCS/DCS/Areas/CE/Utils/CEUtils.cs`
- `DCS/DCS/Areas/CE/Views/FCE001/FCE001E01_Part3List.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE001/FCE001E01_new.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE003/FCE003D01.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE003/FCE003D01_2.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE003/FCE003D01_3.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE003/FCE003D01_5.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE003/FCE003D01_6.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE003/FCE003D07.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E01.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E01_2.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E01_3.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E01_5.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E01_6.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E07.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE004/FCE004E08.cshtml`
- `DCS/DCS/Areas/CE/Views/FCE008/FCE008C04.cshtml`

**GE / LP / PP**

- `DCS/DCS/Areas/GE/Controllers/FSV001Controller.cs`
- `DCS/DCS/Areas/GE/Resources/CED94ShortLabel.Designer.cs`
- `DCS/DCS/Areas/GE/Resources/CED94ShortLabel.resx`
- `DCS/DCS/Areas/GE/Scripts/FAD001E01.js`
- `DCS/DCS/Areas/GE/Scripts/FAD001S01.js`
- `DCS/DCS/Areas/GE/Scripts/FAD002E01.js`
- `DCS/DCS/Areas/GE/Scripts/FAD002S01.js`
- `DCS/DCS/Areas/GE/Scripts/FAD003E01.js`
- `DCS/DCS/Areas/GE/Scripts/FAD003S01.js`
- `DCS/DCS/Areas/GE/Scripts/FCD009S01.js`
- `DCS/DCS/Areas/GE/Scripts/FCD010S01.js`
- `DCS/DCS/Areas/GE/Scripts/FCD024S01.js`
- `DCS/DCS/Areas/GE/Scripts/FCD036S01.js`
- `DCS/DCS/Areas/LP/Controllers/FLP008Controller.cs`
- `DCS/DCS/Areas/LP/Controllers/FLP019Controller.cs`
- `DCS/DCS/Areas/LP/Models/Dao/LPMaintDao.cs`
- `DCS/DCS/Areas/LP/Scripts/FLP028S01.js`
- `DCS/DCS/Areas/LP/Views/FLP022/FLP022S01FilterRuleForm.cshtml`
- `DCS/DCS/Areas/PP/AP/Scripts/FCA004S01.js`
- `DCS/DCS/Areas/PP/AP/Scripts/FCA007S01.js`
- `DCS/DCS/Areas/PP/AP/Scripts/FPV004S01.js`
- `DCS/DCS/Areas/PP/AP/Scripts/FSS003S01.js`
- `DCS/DCS/Areas/PP/EP/Models/Dao/EPMaintDao.cs`
- `DCS/DCS/Areas/PP/EP/Scripts/FPE301S01.js`
- `DCS/DCS/Areas/PP/EP/Views/FDA002/FDA002E18.cshtml`
- `DCS/DCS/Areas/PP/EP/Views/FDA005/FDA005E18.cshtml`
- `DCS/DCS/Areas/PP/PE/Controllers/FPC009Controller.cs`
- `DCS/DCS/Areas/PP/PE/Models/Dao/PEEnqDao.cs`
- `DCS/DCS/Areas/PP/PE/Models/Dao/PEMaintDao.cs`
- `DCS/DCS/Areas/PP/PE/Models/Model/FPC009/FPC009E01Model.cs`
- `DCS/DCS/Areas/PP/PE/Models/Model/FPC009/FPC009S01Model.cs`
- `DCS/DCS/Areas/PP/PE/Models/Model/FPC009/FPC009S01RecordModel.cs`
- `DCS/DCS/Areas/PP/PE/Scripts/FPC008S01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPC009E01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPC009S01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE006E01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE006S02.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE007S01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE013S01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE017S06.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE026E01.js`
- `DCS/DCS/Areas/PP/PE/Scripts/FPE026E60.js`
- `DCS/DCS/Areas/PP/PE/Views/FPC009/FPC009E01.cshtml`
- `DCS/DCS/Areas/PP/PE/Views/FPC009/FPC009E02.cshtml`
- `DCS/DCS/Areas/PP/PE/Views/FPC009/FPC009S01.cshtml`
- `DCS/DCS/Areas/PP/PE/Views/FPE022/FPE022S01FilterRuleForm.cshtml`

**Scripts / content / packages (shared edits, not listed file-by-file above)**

Remaining shared edit rows are jQuery / fullcalendar / unobtrusive-validation content under `DCS/DCS/Content`, `DCS/DCS/Scripts`, and `DCS/packages/...` (same relative path in both manifests).

### 6.3 Shared delete files (57) -- identical set

Old jQuery 2.1.3 and jQuery UI 1.11.2 artifacts. Same relative paths in A and B.

```
DCS/DCS/Scripts/jquery-2.1.3.intellisense.js
DCS/DCS/Scripts/jquery-2.1.3.js
DCS/DCS/Scripts/jquery-2.1.3.min.js
DCS/DCS/Scripts/jquery-2.1.3.min.map
DCS/DCS/Scripts/jquery-ui-1.11.2.js
DCS/DCS/Scripts/jquery-ui-1.11.2.min.js
DCS/packages/Microsoft.jQuery.Unobtrusive.Validation.3.0.0/Content/Scripts/jquery.validate.unobtrusive.js
DCS/packages/Microsoft.jQuery.Unobtrusive.Validation.3.0.0/Content/Scripts/jquery.validate.unobtrusive.min.js
DCS/packages/Microsoft.jQuery.Unobtrusive.Validation.3.0.0/Microsoft.jQuery.Unobtrusive.Validation.3.0.0.nupkg
DCS/packages/jQuery.2.1.3/Content/Scripts/jquery-2.1.3-vsdoc.js
DCS/packages/jQuery.2.1.3/Content/Scripts/jquery-2.1.3.js
DCS/packages/jQuery.2.1.3/Content/Scripts/jquery-2.1.3.min.js
DCS/packages/jQuery.2.1.3/Content/Scripts/jquery-2.1.3.min.map
DCS/packages/jQuery.2.1.3/Tools/common.ps1
DCS/packages/jQuery.2.1.3/Tools/install.ps1
DCS/packages/jQuery.2.1.3/Tools/jquery-2.1.3.intellisense.js
DCS/packages/jQuery.2.1.3/Tools/uninstall.ps1
DCS/packages/jQuery.2.1.3/jQuery.2.1.3.nupkg
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/accordion.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/all.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/autocomplete.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/base.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/button.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/core.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/datepicker.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/dialog.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/draggable.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_flat_0_aaaaaa_40x100.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_flat_75_ffffff_40x100.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_glass_55_fbf9ee_1x400.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_glass_65_ffffff_1x400.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_glass_75_dadada_1x400.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_glass_75_e6e6e6_1x400.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_glass_95_fef1ec_1x400.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-bg_highlight-soft_75_cccccc_1x100.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-icons_222222_256x240.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-icons_2e83ff_256x240.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-icons_454545_256x240.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-icons_888888_256x240.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/images/ui-icons_cd0a0a_256x240.png
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/menu.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/progressbar.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/resizable.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/selectable.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/selectmenu.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/slider.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/sortable.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/spinner.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/tabs.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/theme.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Content/themes/base/tooltip.css
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Scripts/jquery-ui-1.11.2.js
DCS/packages/jQuery.UI.Combined.1.11.2/Content/Scripts/jquery-ui-1.11.2.min.js
DCS/packages/jQuery.UI.Combined.1.11.2/Tools/common.ps1
DCS/packages/jQuery.UI.Combined.1.11.2/Tools/install.ps1
DCS/packages/jQuery.UI.Combined.1.11.2/Tools/uninstall.ps1
DCS/packages/jQuery.UI.Combined.1.11.2/jQuery.UI.Combined.1.11.2.nupkg
```

---

## 7. Checklist before check-in on DUTYSTAMP

1. Confirm the **5 A-only source files** in section 4.1 -- either already present on the branch tip, or still need to be ported.
2. Confirm whether **`Content/themes/base/images`** theme PNGs still need updating, or only the NuGet package copies.
3. Confirm whether **`CommonCipher.dll`** should be added on B.
4. Confirm the **`Web.config`** edit on B is intentional for `DEV-UPGRADE-DUTYSTAMP`.
5. The 14 A-only package **folder** adds are usually TFS folder-node noise and are low risk if the files under them already exist in B.
