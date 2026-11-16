# 📘 School Term Marks System

A complete, **offline-first** term test marks management system for schools. Built with pure HTML, CSS and JavaScript — **no server, no build step, no internet required** (after first load). Track marks, ranks, averages and progress reports, print report cards, and optionally sync to **Google Sheets**.



![Version](https://img.shields.io/badge/version-3.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Offline](https://img.shields.io/badge/offline-first-brightgreen)
![Lang](https://img.shields.io/badge/languages-English%20%7C%20සිංහල-purple)

---

## 📸 Screenshots

### 1. Dashboard
![Dashboard](screenshot%2001.png)
*Live KPIs, exam-trend chart, top performers, grade distribution and most-improved students.*

### 2. Class Marks Table
![Class View](screenshot%2002.png)
*Rank, per-subject marks, totals, averages, grades, inline quick-edit, bulk entry and CSV export.*

### 3. Student Progress Report & Admin Panel
![Report / Admin](screenshot%2003.png)
*A4-printable progress report and the admin panel for school profile, grades, subjects and Google Sheets sync.*


> 💡 **Add these images** to a `screenshots/` folder in the repo root. Recommended size: **1440 × 900 px**, PNG.

---

### 🚀 **[▶ Try the Live Demo](https://enchanting-blancmange-9a34ee.netlify.app)**

---

## ✨ Features

| | |
|---|---|
| 🎓 **Multi-grade** | Grades 1 – 13, each with its own subject list |
| 📊 **Live dashboard** | KPIs, trend charts, top performers, grade distribution, most-improved |
| 🏫 **Class view** | Ranked marks table, per-subject stats (avg / max / min / pass % / absent), year-rank mode |
| 👤 **Student profiles** | Full exam history, strengths / weaknesses, trend chart vs class average |
| 📄 **Printable reports** | A4 report cards with grades, rank, remarks, signature lines |
| 📥 **Bulk entry** | Paste a whole column of marks per subject (Excel-friendly) |
| 📤 **CSV import / export** | Download per-grade templates, import marks from CSV |
| ☁️ **Google Sheets sync** | Pull marks from a public sheet; push back via Apps Script |
| 🔐 **Admin / guest roles** | Guests can fill blank marks; admins can do everything |
| 🌐 **English + Sinhala** | Full UI translation, instant switch |
| 🌙 **Dark mode** | One-click theme toggle, remembered per browser |
| 💾 **Offline-first** | Everything runs from `localStorage`; works without internet after first load |
| 🧪 **Demo data** | Sample students pre-loaded so you can try everything before committing |
| 🔄 **Auto-push queue** | Offline changes are queued and pushed when you're back online |
| 🖨 **A4 print** | Class marks table (landscape) and student report (portrait) |

---

## 🚀 Quick Start

1. **Download** or clone this repository.
2. Open **`index.html`** in **Chrome** or **Edge**.
3. That's it — no server, no install, no account needed.

The system starts with **demo data** (≈50 students across Grades 6–8) so you can click around immediately. Demo data is removed automatically the moment you connect a real Google Sheet or import a CSV.

---

## 🔐 Default Admin Login

| Field | Value |
|---|---|
| Username | `admin` |
| Password | `24031` |

> ⚠️ **Change this immediately** after first login: **Admin → General → Admin login details**.

### Guest vs Admin

**Guests** (not logged in) can:
- View the dashboard, classes, students and reports
- Fill **blank** marks
- Update marks **they entered themselves** in this session

**Guests cannot**: delete records, edit older marks, create terms, or change settings.

---

## ⚙️ Full Configuration — A to Z

### 1. First-time setup (Admin panel)

Click **Admin Login** in the top-right corner and sign in. Then work through the left sidebar tabs.

#### 1.1 School profile — *Admin → General*

- **School name** — shown in the header, hero banner and every printed report.
- **Logo** — upload any image (PNG/JPG). It's automatically resized to 120 px height and stored as base64 in `localStorage`.

#### 1.2 Admin login details — *Admin → General*

- Change **username** and **password** (min 4 characters).
- Stored locally in your browser's `localStorage`. **Not** encrypted — treat this as a **local admin PIN**, not a real auth system.

#### 1.3 Grades & subjects — *Admin → Grades & subjects*

- **Enable / disable grades** — 1 to 13. A grade with existing records cannot be disabled (you'll be warned).
- **Subjects per grade** — each grade has its own list. For each grade:
  - Add / remove / reorder subjects
  - Rename a subject
  - Add an optional **display title** using the `Name | Display title` syntax:
    ```
    Civic Education | Basket 1
    Art/Dancing | Basket 2
    ```
    The real name (`Civic Education`) is used internally; `Basket 1` is what students and parents see.
  - **Copy subjects from grade** — quickly clone a subject list from any other grade
  - **Apply to all grades** — push the current list to every grade
  - **Remove subject warning** — if a removed subject already has marks, you'll be asked to confirm (those marks will be deleted).

**Default subject list:**

```
Mathematics, First Language, Religion, Science, English,
History, Geography, ICT, Art, Health & PE
```

**Auto-aliases for grades ≥ 10:**

```
Civic Education   → Basket 1
Art/Dancing       → Basket 2
Home Science      → Basket 3
```

#### 1.4 Create a new term — *Admin → Students & terms* or `🗓 New term`

- Pick **grade**, **year**, **term** (1, 2, or 3).
- The system **copies the student list** from:
  1. The previous term of the same year (if exists), OR
  2. The same year of the previous grade (for a new academic year), OR
  3. The most recent term of the same grade.
- Marks stay blank — enter them afterwards.
- Use **Add students** for the very first term.

#### 1.5 Add students — *Admin → Students & terms*

Paste a list, **one per line**:

```
0123, Amara Perera
0124, Nimal Silva
0125, Kavindu Fernando
```

or just names:

```
Amara Perera
Nimal Silva
```

- If you include a term = **All terms of this year**, the student is added to every existing term of that year.
- Duplicates are detected by **admission no** (if present) or by **fuzzy name matching** (case/space/punctuation-insensitive, with 1-character edit tolerance for long names).

#### 1.6 Entering marks

Three ways:

| Method | Where | Use when |
|---|---|---|
| **Add marks** | Class view → `＋ Add marks` | One student, one exam |
| **Quick edit** | Class view → `✏️ Quick edit` | Many students, inline |
| **Bulk entry** | Class view → `📥 Bulk entry by subject` | Whole class, one subject |

**Mark rules:**
- `0 – 100` — valid mark
- `AB` — absent (counts as 0 in totals, but displayed as "AB")
- Empty — not yet entered
- Grade thresholds (default pass = 35): **A ≥ 75, B ≥ 65, C ≥ 50, S ≥ 35, W < 35**

#### 1.7 Bulk entry — fastest way to key in a class

1. Choose grade / term / subject.
2. Paste one mark per line — **same order as the names on the left**.
3. `AB` = absent, blank line = keep existing value.
4. You can paste a whole **column** directly from Excel / Google Sheets.
5. Locked cells (marks entered by another guest, or older marks) are shown with 🔒 and skipped.

The counter at the top shows `entered / total`, invalid line numbers, and ignored extra lines.

---

### 2. Google Sheets sync (optional, but powerful)

You can use the app **completely offline**, or connect a Google Sheet per grade so that:

- **Pull** = the app reads data from the sheet → stored in `localStorage`.
- **Push** = the app writes its data to the sheet (via Apps Script).

#### 2.1 Sheet column layout

Every sheet must have this exact header row:

```
Year | Admission No | Name | Term | <subject 1> | <subject 2> | ... | Total Marks | Average | Position
```

- The first four columns (`Year`, `Admission No`, `Name`, `Term`) are **fixed** — don't rename or reorder them.
- Any number of subject columns follow.
- `Total Marks`, `Average`, `Position` are **calculated by Apps Script** on push — you can leave them blank.
- Admission numbers like `0123` are preserved as **text** (leading zeros kept).

#### 2.2 Six-step first-time setup

> Follow **Admin → Google Sheets → Connect Google Sheets — first time** in the app. Same steps here.

**Step 1 — Download templates**
- In **Admin → Google Sheets**, click **⬇ Download templates for all grades (.zip)**.
- You get one CSV file per enabled grade (`Grade_6_Term_Test_Results.csv`, etc.).
- Extract the ZIP.

**Step 2 — Upload to Google Drive**
- Go to [drive.google.com](https://drive.google.com) → **New → File upload** → upload all CSVs.

**Step 3 — Convert to Google Sheets**
- Right-click each file → **Open with → Google Sheets**.
- If prompted, use **File → Save as Google Sheets**.

**Step 4 — Share each sheet**
- Open the sheet → **Share → General access → "Anyone with the link"** → role **Editor** → **Copy link**.

**Step 5 — Paste links into the app**
- In **Admin → Google Sheets**, paste each link into the matching grade box.
- Press **⬇ (Pull)** to fetch the data. This removes any demo data automatically.

**Step 6 — (Optional) Enable Push via Apps Script**
- One-time setup; see below.

#### 2.3 Apps Script setup (for Push)

Push writes the app's data back into your sheet. You need a tiny Apps Script Web App.

**Step 1** — Go to [script.google.com](https://script.google.com) → **New project**.

**Step 2** — Replace the contents of `Code.gs` with the code shown in **Admin → Google Sheets** (or from this repo's `Code.gs` file):

```javascript
function col(n){var s='';while(n>0){var m=(n-1)%26;s=String.fromCharCode(65+m)+s;n=Math.floor((n-1)/26)}return s}
function doPost(e){
  var d=JSON.parse(e.postData.contents),sh=SpreadsheetApp.openById(d.id).getSheets()[0],s=d.sc,f=d.fc||3,out=[];
  d.rows.forEach(function(r,i){var n=i+2;
    out.push(r.slice(0,f+s).concat(['=SUM('+col(f+1)+n+':'+col(f+s)+n+')','='+col(f+s+1)+n+'/'+s,r[f+s]]));});
  sh.clear();
  sh.getRange(1,2,out.length+1,1).setNumberFormat('@'); // keep admission numbers like 0123
  sh.getRange(1,1,1,d.head.length).setValues([d.head]);
  if(out.length)sh.getRange(2,1,out.length,d.head.length).setValues(out);
  return ContentService.createTextOutput('ok');
}
function doGet(){return ContentService.createTextOutput('OK');}
```

**Step 3** — **Deploy → New deployment**
- Type: **Web app**
- Description: anything
- Execute as: **Me**
- Who has access: **Anyone**

**Step 4** — Copy the **Web app URL** (ends in `/exec`) and paste it into **Admin → Google Sheets → Apps Script Web App URL**.

**Step 5** — Tick **Auto-push on every change** if you want changes sent to the sheet automatically (1.5 s debounce). Otherwise use the **⬆ Push all** button or the **⬆ N unsynced** pill in the header.

> ⚠️ **Push replaces the entire first sheet** with the app's data. If the sheet has newer data, **Pull first**.

#### 2.4 Pull vs Push vs Offline

| | Reads | Writes | Needs internet |
|---|---|---|---|
| **Pull** | ✅ Sheet → App | | ✅ |
| **Push** | | ✅ App → Sheet | ✅ |
| **Offline use** | ✅ localStorage | ✅ localStorage | ❌ |

When offline, changes are **queued** (`DB.cfg.pend`). The header shows `⬆ N unsynced`. On reconnect:
- If **Auto-push** is on → pushes automatically.
- Otherwise → click the **⬆ N unsynced** pill.

---

### 3. Backup & restore — *Admin → Data*

- **Backup** — downloads the entire `localStorage` database as `term_marks_backup.json`.
- **Restore** — reads that JSON file back in (overwrites everything).
- **Reset to original data** — wipes the browser and starts fresh (asks for confirmation).
- **Import CSV** — per-grade CSV import (same column layout as templates).
- **CSV template** — download a blank template for the currently selected grade.
- **Remove demo data** — deletes all records flagged as `demo`.

> 💡 **Take a backup regularly.** `localStorage` is per-browser. Clearing cache/cookies or switching devices = lost data.

---

### 4. Language, theme and header

- **EN / සිං** toggle — full UI translation, including all toast messages, form labels and printable reports.
- **🌙 / ☀️** — dark / light theme, remembered in `localStorage`.
- **● Online / Offline** pill — live network status.
- **🛡 Admin** tag — visible only when signed in.

---

### 5. Guest mode & permissions

The system deliberately allows **partial editing without login**, so teachers can help key in marks on a shared machine.

| Action | Guest | Admin |
|---|---|---|
| View everything | ✅ | ✅ |
| Fill a blank mark | ✅ | ✅ |
| Change a mark they themselves entered | ✅ | ✅ |
| Change a mark entered by another guest | ❌ | ✅ |
| Change older admin marks | ❌ | ✅ |
| Add a new student | ❌ | ✅ |
| Create a new term | ❌ | ✅ |
| Delete a record | ❌ | ✅ |
| Edit grade/subject config | ❌ | ✅ |
| Import / export / backup | ❌ | ✅ |

Guest marks are tracked in `r.gm` (guest-mark flags) so the app knows which cells are still editable.

---

## 📁 File Structure

```
school-term-marks/
├── index.html            # Main shell
├── style.css             # All styles (light + dark, print, animations)
├── core.js               # DB, auth, calc, Google Sheets, ZIP, demo data
├── views.js              # All screens (dash / classes / students / compare / admin / report / login)
├── app.js                # Event handlers, actions, modals, bulk entry
├── i18n.js               # English + Sinhala translations
├── gs.js                 # Apps Script code embedded as a JS string
├── Code.gs               # Standalone Apps Script (copy-paste into script.google.com)
├── README.txt            # Quick-start text used by the app
└── screenshots/          # README images
    ├── dashboard.png
    ├── class-view.png
    ├── student-report.png
    └── admin-panel.png
```

---

## 🧠 How It Works

- **Storage** — `localStorage` under the key `tm3_db`. Persisted on every change (300 ms debounce) and on `beforeunload` / `pagehide` / `visibilitychange`.
- **Student identity** — records from different grades/terms are merged into a **single student** by:
  1. Exact admission number match, OR
  2. Fuzzy name match (case/space/punctuation-insensitive, 1-char tolerance for names > 8 chars)
- **Ranking** — computed per grade × year × term, with tie-sharing (students with the same total share the same rank).
- **Average** — `total marks ÷ number of subjects` (subjects not entered count as 0).
- **Grade** — A/B/C/S/W thresholds, admin-configurable pass mark (default 35).
- **Google Sheets pull** — tries CSV export first, falls back to `gviz/tq` JSONP (works around CORS).
- **Google Sheets push** — `fetch` with `mode: 'no-cors'` to the Apps Script `/exec` URL. Apps Script recalculates `Total`, `Average`, `Position` with real formulas, so the sheet stays "live".

---

## 🔒 Security Notes (read this)

This is a **client-side app** for trusted environments (a school office, a classroom laptop, a teacher's PC):

- The admin password is stored **in plain text** in `localStorage`. It prevents accidental edits, not determined attackers. Treat it as a **local PIN**.
- Google Sheets links must be **"Anyone with the link → Editor"** for the app to read and push. That means **anyone with the URL can edit the sheet**. Keep sheet URLs private; share this app only with staff.
- Backups are plain JSON — treat `term_marks_backup.json` as sensitive student data.
- There is **no server, no telemetry, no analytics, no third-party tracking**. Your data never leaves the browser unless **you** connect a Google Sheet.

---

## 🧪 Demo Data

A fresh install starts with ~50 sample students across Grades 6, 7, 8 with three terms of marks — enough to see the dashboard, charts, ranks and reports in action.

Demo data is removed automatically when you:
- Paste a Google Sheet link and Pull, OR
- Import a CSV, OR
- Click **Admin → Data → Remove demo data**.

You can reload it any time from **Admin → Data → Load demo data**.

---

## 🖨 Printing

- **Class view → 🖨** — prints the marks table (landscape, A4).
- **Student → 📄 Report** — prints a formal progress report (A4) with:
  - School name + logo
  - Student name, admission no, grade, exam
  - Per-subject marks, best mark in class, position, grade
  - Totals, average, class rank, remark (r1–r5)
  - Signature lines for class teacher / principal / parent

Both use the `@page` and `.pt` (print-only) styles in `style.css`, and hide the header, footer, demo banner and toast.

---

## 🐞 Troubleshooting

| Problem | Fix |
|---|---|
| "Could not read the sheet" on Pull | Make sure the sheet is **"Anyone with the link → Editor"**, and the header row has `Year`, `Admission No`, `Name`, `Term` in the first four columns |
| "Set the Google Sheet link for this grade first" | Paste the link/ID into **Admin → Google Sheets** for that specific grade |
| Push shows no error but nothing happens | Apps Script must be deployed as **Web app**, **Execute as: Me**, **Access: Anyone**. Re-deploy after any code change |
| Admission numbers lose leading zeros | The Apps Script forces column B to text format. Re-deploy the current `Code.gs` |
| Data disappeared | Check `localStorage` wasn't cleared. Use **Admin → Data → Restore** with your latest JSON backup |
| Sinhala fonts look wrong | Use Chrome/Edge with `Iskoola Pota` or `Nirmala UI` installed (standard on Windows) |
| Old data loads on a new device | `localStorage` is per-browser. Export a backup on the old device, restore on the new one |
| Charts don't render | Make sure `Chart.js` (loaded in `index.html`) is available — the first load needs internet for the CDN; after that it's cached |
| "Admin permission required" for action | Only guests see this — log in as admin to unlock the action |

---

## 🌐 Browser Support

| Browser | Status |
|---|---|
| Chrome (desktop & Android) | ✅ Recommended |
| Edge (desktop) | ✅ Recommended |
| Firefox | ✅ Works |
| Safari (macOS / iOS) | ✅ Works |
| Internet Explorer | ❌ Not supported |

---

## 📋 Google Sheet Header Reference

For a grade with subjects *Mathematics, Science, English*:

| A | B | C | D | E | F | G | H | I | J |
|---|---|---|---|---|---|---|---|---|---|
| Year | Admission No | Name | Term | Mathematics | Science | English | Total Marks | Average | Position |
| 2025 | 0123 | Amara Perera | 1 | 85 | 78 | 92 | *(auto)* | *(auto)* | *(auto)* |

On **Push**, columns **H, I, J** are filled with real Excel formulas by the Apps Script.

---

## 📌 Quick checklist — from zero to production

- [ ] Open `index.html` in Chrome
- [ ] Log in as `admin / 24031`
- [ ] **Admin → General** — set school name, upload logo
- [ ] **Admin → General** — change admin password
- [ ] **Admin → Grades & subjects** — enable only the grades you need, adjust subjects
- [ ] **Admin → Students & terms** — create your first term, paste student list
- [ ] Enter marks (Quick edit or Bulk entry)
- [ ] *(optional)* **Admin → Google Sheets** — download templates, create sheets, paste links, Pull
- [ ] *(optional)* Deploy Apps Script, paste URL, enable Auto-push
- [ ] **Admin → Data → Backup** — save your `term_marks_backup.json`
- [ ] Share the app + staff PIN with your teachers

That's it — you're running. 🎉

---

## 🤝 Contributing

1. Fork this repo
2. Create your feature branch: `git checkout -b feature/amazing-thing`
3. Commit your changes: `git commit -m 'Add amazing thing'`
4. Push: `git push origin feature/amazing-thing`
5. Open a Pull Request

Please keep the app **dependency-free** (other than Chart.js) and **offline-first**.

---

## 📄 License

This project is licensed under the **MIT License** — see the `LICENSE` file for details. If no license file exists yet, add one (MIT is a good default).

---

## 🙏 Credits

- **Author**: [Sampath Tharanga](https://github.com/SampathTharanga)
- **Charts**: [Chart.js](https://www.chartjs.org/)
- **Fonts**: Inter, Noto Sans Sinhala

Made with ❤️ for Sri Lankan schools.

---

## ⭐ Support

If this project helped you, please give it a ⭐ on GitHub — it means a lot!

For bug reports and feature requests, open an issue on the repository.
