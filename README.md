# AEM & TESS Comparison and Ship Schedule Management System

A client-side web application suite built for managing, comparing, and analyzing cruise ship activities, itineraries, schedules, and dual-file search operations between Adobe Experience Manager (AEM) data and TESS master files.

---

## 🚀 Key Features & Modules

### 1. Activities Comparison Tab (`Activities Comparison`)
- **AEM vs TESS Match Engine**: Matches uploaded daily AEM CSV exports against the TESS master Excel file (`Activities` sheet).
- **Match Criteria**: Compares records across Day, Start/End Time, Venue, Headline/Title, Category, and AEM ID.
- **Service Mark Normalization**: Automatically strips registered trademarks and service marks (`℠`, `™`, `®`, `©`, `SM`, `TM`) during comparisons to prevent false mismatches.
- **Time Standardization**: Auto-normalizes times (`midnight` → `12:00 am`, `noon` → `12:00 pm`, fractional Excel decimal times, lowercase `am`/`pm`).
- **Filter Status Options**:
  - All Records
  - Clean Matches Only
  - Mismatches Only
  - Missing in TESS Only
  - **Mismatches & Missing** (unified view of discrepancies)
- **Interactive Checkbox Strike-through**: First column checkbox strikes through completed rows (`row-struck`); persists state across reloads via dual storage (`localStorage` + cookies).
- **Resizable & Filterable Columns**: Column drag-resizers with per-column text filtering dropdowns.
- **CSV Report Export**: Export detailed comparison reports with mismatch flags.

---

### 2. TESS File Data Viewer (`TESS file`)
- **Raw Master View**: Shows all records uploaded from the TESS master file sorted chronologically in ascending order of start time.
- **Per-Column Filtering & Resizing**: Independent column filter inputs with reset shortcuts and column drag resizing.
- **Interactive Checklist**: Dedicated checkbox column with strike-through and persistence.

---

### 3. Dual Live Search (`CSV Dual Search`)
- **Dual-Engine Search**: Simultaneously searches across two independent datasets (CSV or multi-tab Excel files).
- **Multi-Token AND Search**: Fast multi-token matching across all fields or targeted columns.
- **Integrated In-Canvas View**: Full native inlined implementation without `iframe` isolation issues, occupying 100% of the available canvas.

---

### 4. Ship Schedule & Rank Voyage Filter (`Rank Filter`)
- **Ship Selector**: Automatically parses ship names from **Row 3** of schedule sheets (defaults to `Serenade` or any detected vessel) and displays all schedule records for the selected ship.
- **Day# Auto-Sequencing**: Positioned between *Berth Date* and *Day*. Counts sequentially from `1` and automatically resets back to `1` upon reaching a turnaround record where `RANK = T`.
- **Voyage Assignment**:
  - Automatically groups days into voyages (`Voyage 1`, `Voyage 2`, etc.).
  - Configurable initial voyage starting number.
  - Automatically advances the voyage number following every row with `RANK = T`.
- **Repeated Locations (Itinerary Pattern Matching)**:
  - Compares the entire multi-day port sequence across all $x$ days of each voyage.
  - If two or more voyages share the exact same sequence of ports over their entire duration, the matching voyage numbers are shown (with detailed tooltips).
- **Duration Calculation**:
  - Calculates the total voyage duration (in days) on `Rank T` turnaround rows.
  - Computes elapsed calendar days between consecutive berth dates on individual port days.
- **Deadline & Lockout Alerts**:
  - **Content Deadline (-14 Days)**: Computes the date 14 days prior to the Berth Date.
  - **TESS Lockout (-7 Days)**: Computes the date 7 days prior to the Berth Date.
  - **Red Alert Highlighting**: Unchecked rows within the deadline window or overdue are automatically highlighted with soft red backgrounds. Checking the row clears the alert and strikes through the row.
- **Custom Notes**: Includes `Notes 1` and `Notes 2` input fields per row with persistent storage.
- **Ultra-Compact Columns & Smooth Resizing**:
  - Synchronized `<colgroup>` and `<th>` column drag handles.
  - Compact widths (Berth Date tightly formatted at 54px).
  - Built-in horizontal and vertical scrollbars directly alongside the table.
- **CSV Export**: Export filtered schedule and voyage data directly to `.csv`.

---

### 5. MS Excel-Style Bottom Navigation Bar
- Positioned permanently at the bottom of the viewport (`sticky` / docked).
- Quick sheet-switching between all active modules:
  1. `Activities Comparison`
  2. `TESS file`
  3. `CSV Dual Search`
  4. `Rank Filter`

---

## 🛠️ Technology Stack

- **HTML5 & CSS3**: Responsive flexbox layout, custom scrollbars, sticky headers, and Excel sheet tab styling.
- **JavaScript (Vanilla ES6+)**: Client-side reactive parsing, DOM manipulation, and drag resizing without heavy frameworks.
- **SheetJS (xlsx.full.min.js)**: Multi-sheet Excel workbook parsing and cell inspection.
- **PapaParse**: High-performance streaming CSV parser.
- **FontAwesome 6**: Intuitive UI icons and navigation controls.
- **Tailwind CSS (utility CDN)**: Utilized within embedded tools and helper modules.

---

---

## 💡 How to Use

1. **Open Application**:
   - Open `AEM and TESS.html` in any modern web browser (Google Chrome, Microsoft Edge, Firefox).
2. **Upload Files**:
   - Use the collapsible left sidebar to upload AEM daily CSV files and the TESS master Excel workbook.
   - For schedule filtering, switch to the **Rank Filter** tab and select your schedule Excel file.
3. **Compare & Review**:
   - Click **Compare Records** to run the diff engine.
   - Use column filters and status dropdowns to isolate mismatches or missing activities.
   - Check off rows as you verify them; your checklist state is saved automatically.
4. **Export**:
   - Download CSV reports for documentation or sharing with operations teams.

---

## 👤 Author
- **Glen Rajadurai Pauldiraviam**
- Contact: [glenrajadurai24@gmail.com](mailto:glenrajadurai24@gmail.com)
