
# Pattern: SPA File Upload for KPI Tables

## Overview
A Single Page Application (SPA) allows users to upload an Excel file from their desktop.  
The SPA parses the file client-side (using a library like SheetJS) and renders tables dynamically in the browser.  

No backend or API is required — all processing occurs locally in the user’s browser.  

---

## Strengths ✅
- **Low development effort** – only front-end code required.  
- **Secure by default** – nothing leaves the user’s machine.  
- **Flexible** – supports multiple sheets/tables as long as rules are followed.  
- **No backend maintenance** – no servers, databases, or APIs.  
- **Portable** – works offline, simply open the HTML.  

---

## Formatting Rules
- **Row 1 (A1)** → description text (e.g. *“We price within our risk appetite”*).  
- **Row 2** → table headers (`KPI Name | Proposed | Base Figures | …`).  
- **Row 3+** → table data.  

Each sheet is rendered as:  
- Sheet title (from the worksheet name).  
- Description (from A1).  
- Table (from row 2 onward).  

---

## Potential Objections ⚠️

### 1. Manual Upload Step
- **Objection:** *“It’s clunky to upload the spreadsheet each time.”*  
- **Response:** For internal or infrequent updates, this is fine. If daily automation is needed, move to an API integration (future option).  

### 2. Formatting Dependency
- **Objection:** *“If someone misformats the Excel, it will break.”*  
- **Response:** Define clear rules (A1 = description, Row 2 = headers). Add SPA validation to warn if the file doesn’t meet expectations.  

### 3. Version Control
- **Objection:** *“We can’t track which version of the Excel is being used.”*  
- **Response:** Include metadata in the Excel (e.g. Version ID, Created On) and display it in the SPA.  

### 4. Scalability
- **Objection:** *“What if the file is very large?”*  
- **Response:** SheetJS can handle several MBs of data. For very large datasets, use pagination or virtual scrolling.  

### 5. User Error
- **Objection:** *“Users might upload the wrong file.”*  
- **Response:** Validate file name/version in the SPA (e.g. “Unrecognised KPI pack”).  

### 6. Security / Compliance
- **Objection:** *“We don’t want users uploading arbitrary files.”*  
- **Response:** Parsing happens entirely client-side — no data leaves the browser. Risk is minimal unless the Excel is malicious, which is mitigated by browser sandboxing.  

---

## Where This Pattern Works Best
- Internal governance dashboards (e.g. KPI packs).  
- Prototypes where backend investment is not justified.  
- Offline-first tools (works by double-clicking an HTML file).  

## Where It Falls Short
- When the dataset changes very frequently and must always be “live” for all users.  
- When strict validation, audit, or multi-user workflows are required.  
- For very large enterprise-scale datasets (hundreds of thousands of rows).  

---

## Conclusion
This is a **valid, low-cost, secure pattern** for governance dashboards and similar internal tools.  
Future evolution (if needed) could include:  
- Centralised API for always-live data.  
- Automated validation of Excel input.  
- JSON export/import features.  
