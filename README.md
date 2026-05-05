# 🏛️ Barangay Sibaguan — KK Profiling System

**Developer:** Roniel Nyke Gonzales  
**Company:** Lambunao Web Developer  
**Year:** 2026  
**Location:** Barangay Sibaguan, Philippines

---

## 📑 Table of Contents

1. [📁 Files Overview](#-files-overview)
2. [🎯 Project Description](#-project-description)
3. [🔗 How the Two Files Connect](#-how-the-two-files-connect)
4. [⚙️ Google Apps Script Setup (Para Gumana ang Cloud Sync)](#%EF%B8%8F-google-apps-script-setup-para-gumana-ang-cloud-sync)
   - [Step 1: Create Google Sheet](#step-1-create-google-sheet)
   - [Step 2: Create Apps Script](#step-2-create-apps-script)
   - [Step 3: Deploy as Web App](#step-3-deploy-as-web-app)
   - [Step 4: Copy the Web App URL](#step-4-copy-the-web-app-url)
   - [Step 5: Update Your HTML Files](#step-5-update-your-html-files)
5. [📊 Data Flow Architecture](#-data-flow-architecture)
   - [User Submission Flow](#user-submission-flow)
   - [Admin Dashboard Flow](#admin-dashboard-flow)
   - [Real-Time Sync Flow](#real-time-sync-flow)
   - [Offline Fallback Flow](#offline-fallback-flow)
6. [🔐 Security Features](#-security-features)
7. [📧 EmailJS Integration](#-emailjs-integration)
8. [🎵 Voice & Sound Effects](#-voice--sound-effects)
9. [🎨 UI/UX Features](#-uiux-features)
10. [📱 Responsive Design](#-responsive-design)
11. [🗂️ Database Schema](#%EF%B8%8F-database-schema)
12. [🔧 Troubleshooting](#-troubleshooting)
13. [📞 Support](#-support)

---

## 📁 Files Overview

| File | Description | Role |
|------|-------------|------|
| `index.html` | Public KK Profiling Form (User-facing) | **Frontend — User Portal** |
| `admin.html` | Admin Dashboard (Monitor, Approve, Reject) | **Frontend — Admin Portal** |
| `logo.png` | Barangay Logo | **Asset** |
| `image.jpg` | SK Logo | **Asset** |
| `README.md` | Documentation (this file) | **Documentation** |

---

## 🎯 Project Description

Ang **Barangay Sibaguan KK Profiling System** ay isang web-based application na dinisenyo para sa pag-kolekta at pag-manage ng profile ng mga kabataan sa Barangay Sibaguan. Ang system ay sumusunod sa **Republic Act 10742** (Sangguniang Kabataan Reform Act of 2015) na nagtatakda na ang mga miyembro ng Katipunan ng Kabataan (KK) ay dapat na may edad **15-30 years old**.

### 🌟 Key Features

- ✅ **Real-time Data Sync** — Google Sheets + localStorage + BroadcastChannel
- ✅ **Age Validation** — Automatic validation (15-30 years old)
- ✅ **Photo Upload** — ID picture upload with preview
- ✅ **Email Notifications** — EmailJS integration for confirmation emails
- ✅ **Admin Dashboard** — Full CRUD operations with status management
- ✅ **Offline Support** — Queue system for offline submissions
- ✅ **Voice & Sound Effects** — Audio feedback and text-to-speech
- ✅ **Responsive Design** — Mobile-friendly interface
- ✅ **Beautiful Animations** — CSS animations and transitions
- ✅ **Export to CSV** — Data export functionality
- ✅ **Real-time Clock** — Philippine Standard Time display

---

## 🔗 How the Two Files Connect

### Method 1: Google Sheets Web App (Cloud Sync — RECOMMENDED)

Ang form ay nag-su-submit sa isang **Google Apps Script Web App** na nag-store ng data sa Google Sheets. Ang admin dashboard ay nag-read mula sa parehong Google Sheet.

**Advantages:**
- ☁️ Cloud-based storage
- 📊 Easy data analysis via Google Sheets
- 🔄 Real-time sync across devices
- 💾 Automatic backup
- 📱 Accessible anywhere

### Method 2: localStorage + BroadcastChannel (Browser Sync — FALLBACK)

Kung ang Google Sheets ay hindi configured, parehong files ay gumagamit ng **localStorage** at **BroadcastChannel** para mag-sync ng data in real-time sa loob ng parehong browser.

**Advantages:**
- ⚡ Instant sync (no internet required)
- 🔒 Data stays on user's device
- 🆓 No external services needed
- 🚀 Fast performance

---

## ⚙️ Google Apps Script Setup (Para Gumana ang Cloud Sync)

### Step 1: Create Google Sheet

1. **Buksan ang browser** at pumunta sa [Google Sheets](https://sheets.new)
   - O kaya, pumunta sa [Google Drive](https://drive.google.com) at i-click ang **New → Google Sheets**

2. **I-rename ang sheet** sa pangalang: `Barangay Sibaguan KK Profiling`
   - I-click ang title sa taas ("Untitled spreadsheet")
   - I-type ang bagong pangalan
   - I-press **Enter**

3. **I-add ang headers sa Row 1** (Cell A1 hanggang W1):

   | Column | Header Name | Description |
   |--------|-------------|-------------|
   | A | ID | Unique identifier for each member |
   | B | Timestamp | Date and time of submission (ISO format) |
   | C | FullName | Complete name of the member |
   | D | Age | Age in years |
   | E | BirthDate | Date of birth (YYYY-MM-DD format) |
   | F | Gender | Male or Female |
   | G | CivilStatus | Single, Married, Widowed, Separated |
   | H | Purok | Purok/Sitio location (Purok 1-7) |
   | I | Contact | Contact number (Philippine format) |
   | J | Email | Email address |
   | K | Education | Educational attainment |
   | L | Employment | Employment status |
   | M | Skills | Comma-separated list of skills |
   | N | KKBefore | Yes or No (previous KK membership) |
   | O | Programs | Comma-separated list of interested programs |
   | P | EmergencyName | Name of emergency contact |
   | Q | EmergencyContact | Contact number of emergency contact |
   | R | EmergencyRelation | Relationship to emergency contact |
   | S | Comments | Additional comments/suggestions |
   | T | Status | Pending Review / Approved / Rejected |
   | U | FormattedDate | Human-readable date format |
   | V | ApprovedDate | Date when approved (if applicable) |
   | W | IDPictureURL | Base64 encoded image or URL |

4. **I-format ang headers** (Optional pero recommended):
   - I-select ang buong Row 1 (A1:W1)
   - I-click ang **Bold** button (B) sa toolbar
   - I-set ang background color sa light blue (#E3F2FD)
   - I-freeze ang Row 1 (View → Freeze → 1 row)

5. **I-save ang sheet** (automatic na nagsa-save ang Google Sheets)

---

### Step 2: Create Apps Script

1. **Buksan ang Apps Script editor**:
   - Sa loob ng Google Sheet, i-click ang **Extensions** sa menu bar
   - I-hover ang mouse sa **Apps Script**
   - I-click ang **Apps Script** (ito ang magbubukas ng bagong tab)

2. **I-delete ang default code**:
   - Sa Apps Script editor, makikita mo ang default na `function myFunction() {}`
   - I-select lahat ng code (Ctrl+A o Cmd+A)
   - I-delete ang lahat

3. **I-paste ang buong Apps Script code**:

```javascript
/**
 * ============================================================================
 * BARANGAY SIBAGUAN KK PROFILING SYSTEM
 * Google Apps Script — Backend API
 * ============================================================================
 * 
 * This script handles:
 * - POST requests (submit, updateStatus, delete, clearAll)
 * - GET requests (read all data)
 * - OPTIONS requests (CORS preflight)
 * 
 * Author: Roniel Nyke Gonzales
 * Company: Lambunao Web Developer
 * Year: 2026
 */

/**
 * ============================================================================
 * CORS HEADERS CONFIGURATION
 * ============================================================================
 * These headers allow cross-origin requests from any domain.
 * IMPORTANT: For production, restrict the origin to your specific domain.
 */
function getCorsHeaders() {
  return {
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Methods": "POST, GET, OPTIONS",
    "Access-Control-Allow-Headers": "Content-Type"
  };
}

/**
 * ============================================================================
 * DOPOST — HANDLE INCOMING POST REQUESTS
 * ============================================================================
 * This function handles all POST requests from the frontend.
 * 
 * Supported actions:
 * - 'submit'    → Add new member record
 * - 'updateStatus' → Update member status (Pending/Approved/Rejected)
 * - 'delete'    → Delete a member record
 * - 'clearAll'  → Delete ALL member records (USE WITH CAUTION!)
 * 
 * @param {Object} e - The event object containing POST data
 * @returns {TextOutput} JSON response
 */
function doPost(e) {
  const corsHeaders = getCorsHeaders();

  try {
    // Get the active spreadsheet and sheet
    const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
    const sheet = spreadsheet.getActiveSheet();

    // Parse the incoming JSON data
    const data = JSON.parse(e.postData.contents);

    console.log('📥 Received action:', data.action);
    console.log('📦 Data:', JSON.stringify(data));

    // =========================================================================
    // ACTION: SUBMIT — Add new member record
    // =========================================================================
    if (data.action === 'submit') {

      // Prepare the row data array
      const row = [
        data.id || Date.now().toString(),           // A: ID (auto-generate if missing)
        data.timestamp || new Date().toISOString(),  // B: Timestamp
        data.fullName || '',                         // C: FullName
        data.age || '',                              // D: Age
        data.birthDate || '',                        // E: BirthDate
        data.gender || '',                           // F: Gender
        data.civilStatus || '',                      // G: CivilStatus
        data.purok || '',                            // H: Purok
        data.contactNumber || '',                    // I: Contact
        data.email || '',                            // J: Email
        data.education || '',                        // K: Education
        data.employment || '',                       // L: Employment
        Array.isArray(data.skills)                   // M: Skills
          ? data.skills.join(', ') 
          : (data.skills || ''),
        data.kkBefore || '',                         // N: KKBefore
        Array.isArray(data.programs)                 // O: Programs
          ? data.programs.join(', ') 
          : (data.programs || ''),
        data.emergencyName || '',                    // P: EmergencyName
        data.emergencyContact || '',                 // Q: EmergencyContact
        data.emergencyRelation || '',               // R: EmergencyRelation
        data.comments || '',                         // S: Comments
        data.status || 'Pending Review',             // T: Status
        data.formattedDate || new Date().toLocaleString(), // U: FormattedDate
        '',                                          // V: ApprovedDate (empty for new)
        data.idPicture || ''                         // W: IDPictureURL
      ];

      // Append the row to the sheet
      sheet.appendRow(row);

      console.log('✅ New record saved. ID:', row[0]);

      // Return success response
      return ContentService
        .createTextOutput(JSON.stringify({ 
          success: true, 
          message: "Record saved successfully",
          id: row[0]
        }))
        .setMimeType(ContentService.MimeType.JSON)
        .setHeaders(corsHeaders);
    }

    // =========================================================================
    // ACTION: UPDATESTATUS — Update member status
    // =========================================================================
    if (data.action === 'updateStatus') {

      // Get all data from the sheet
      const rows = sheet.getDataRange().getValues();
      let updated = false;

      // Loop through rows starting from row 2 (skip header)
      for (let i = 1; i < rows.length; i++) {
        // Check if the ID matches (Column A = index 0)
        if (String(rows[i][0]) === String(data.id)) {
          // Update Status (Column T = index 19)
          sheet.getRange(i + 1, 20).setValue(data.status);

          // Update ApprovedDate (Column V = index 21)
          sheet.getRange(i + 1, 22).setValue(new Date().toLocaleString());

          updated = true;
          console.log('✅ Status updated. ID:', data.id, '→', data.status);
          break;
        }
      }

      if (!updated) {
        console.warn('⚠️ Record not found for update. ID:', data.id);
      }

      return ContentService
        .createTextOutput(JSON.stringify({ 
          success: true, 
          updated: updated 
        }))
        .setMimeType(ContentService.MimeType.JSON)
        .setHeaders(corsHeaders);
    }

    // =========================================================================
    // ACTION: DELETE — Remove a member record
    // =========================================================================
    if (data.action === 'delete') {

      const rows = sheet.getDataRange().getValues();
      let deleted = false;

      for (let i = 1; i < rows.length; i++) {
        if (String(rows[i][0]) === String(data.id)) {
          // Delete the entire row
          sheet.deleteRow(i + 1);
          deleted = true;
          console.log('🗑️ Record deleted. ID:', data.id);
          break;
        }
      }

      return ContentService
        .createTextOutput(JSON.stringify({ 
          success: true, 
          deleted: deleted 
        }))
        .setMimeType(ContentService.MimeType.JSON)
        .setHeaders(corsHeaders);
    }

    // =========================================================================
    // ACTION: CLEARALL — Delete ALL records (DANGEROUS!)
    // =========================================================================
    if (data.action === 'clearAll') {

      const lastRow = sheet.getLastRow();

      // Only delete if there are data rows (keep header row 1)
      if (lastRow > 1) {
        sheet.deleteRows(2, lastRow - 1);
        console.log('🗑️ All records cleared. Total deleted:', lastRow - 1);
      }

      return ContentService
        .createTextOutput(JSON.stringify({ 
          success: true, 
          cleared: lastRow - 1 
        }))
        .setMimeType(ContentService.MimeType.JSON)
        .setHeaders(corsHeaders);
    }

    // =========================================================================
    // UNKNOWN ACTION
    // =========================================================================
    console.warn('⚠️ Unknown action received:', data.action);

    return ContentService
      .createTextOutput(JSON.stringify({ 
        success: false, 
        error: "Unknown action: " + data.action 
      }))
      .setMimeType(ContentService.MimeType.JSON)
      .setHeaders(corsHeaders);

  } catch (error) {
    // =========================================================================
    // ERROR HANDLING
    // =========================================================================
    console.error('❌ Error in doPost:', error);

    return ContentService
      .createTextOutput(JSON.stringify({ 
        success: false, 
        error: error.message,
        stack: error.stack 
      }))
      .setMimeType(ContentService.MimeType.JSON)
      .setHeaders(corsHeaders);
  }
}

/**
 * ============================================================================
 * DOGET — HANDLE INCOMING GET REQUESTS
 * ============================================================================
 * This function returns ALL member records in JSON format.
 * Used by the admin dashboard to fetch data.
 * 
 * @param {Object} e - The event object (not used but required by Apps Script)
 * @returns {TextOutput} JSON array of all records
 */
function doGet(e) {
  const corsHeaders = getCorsHeaders();

  try {
    const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
    const sheet = spreadsheet.getActiveSheet();

    // Get all data including headers
    const rows = sheet.getDataRange().getValues();

    // First row contains headers
    const headersRow = rows[0];
    const data = [];

    // Loop through data rows (skip header row 0)
    for (let i = 1; i < rows.length; i++) {
      const row = rows[i];
      const obj = {};

      // Map each column to its header
      headersRow.forEach((header, index) => {
        const key = header.toString().trim();
        if (key) {
          obj[key] = row[index];
        }
      });

      // Normalize keys for frontend compatibility
      // This ensures the frontend can access data regardless of header case
      obj.id = row[0];
      obj.timestamp = row[1];
      obj.fullName = row[2];
      obj.age = row[3];
      obj.birthDate = row[4];
      obj.gender = row[5];
      obj.civilStatus = row[6];
      obj.purok = row[7];
      obj.contactNumber = row[8];
      obj.email = row[9];
      obj.education = row[10];
      obj.employment = row[11];
      obj.skills = row[12] ? row[12].toString().split(',').map(s => s.trim()) : [];
      obj.kkBefore = row[13];
      obj.programs = row[14] ? row[14].toString().split(',').map(s => s.trim()) : [];
      obj.emergencyName = row[15];
      obj.emergencyContact = row[16];
      obj.emergencyRelation = row[17];
      obj.comments = row[18];
      obj.status = row[19] || 'Pending Review';
      obj.formattedDate = row[20];
      obj.approvedDate = row[21];
      obj.idPicture = row[22];

      data.push(obj);
    }

    console.log('📤 Returning', data.length, 'records');

    return ContentService
      .createTextOutput(JSON.stringify({ 
        success: true, 
        data: data,
        count: data.length,
        timestamp: new Date().toISOString()
      }))
      .setMimeType(ContentService.MimeType.JSON)
      .setHeaders(corsHeaders);

  } catch (error) {
    console.error('❌ Error in doGet:', error);

    return ContentService
      .createTextOutput(JSON.stringify({ 
        success: false, 
        error: error.message 
      }))
      .setMimeType(ContentService.MimeType.JSON)
      .setHeaders(corsHeaders);
  }
}

/**
 * ============================================================================
 * DOOPTIONS — HANDLE CORS PREFLIGHT REQUESTS
 * ============================================================================
 * Browsers send OPTIONS requests before POST/GET to check CORS permissions.
 * This function responds with the appropriate CORS headers.
 * 
 * @param {Object} e - The event object
 * @returns {TextOutput} Empty response with CORS headers
 */
function doOptions(e) {
  return ContentService
    .createTextOutput("")
    .setMimeType(ContentService.MimeType.JSON)
    .setHeaders(getCorsHeaders());
}

/**
 * ============================================================================
 * HELPER FUNCTIONS (Optional but useful)
 * ============================================================================
 */

/**
 * Get a specific record by ID
 * @param {string} id - The member ID
 * @returns {Object|null} The member record or null
 */
function getRecordById(id) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const rows = sheet.getDataRange().getValues();

  for (let i = 1; i < rows.length; i++) {
    if (String(rows[i][0]) === String(id)) {
      return {
        id: rows[i][0],
        fullName: rows[i][2],
        status: rows[i][19]
      };
    }
  }
  return null;
}

/**
 * Get statistics about the data
 * @returns {Object} Statistics object
 */
function getStatistics() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const rows = sheet.getDataRange().getValues();

  const total = rows.length - 1; // Exclude header
  let approved = 0, pending = 0, rejected = 0;

  for (let i = 1; i < rows.length; i++) {
    const status = rows[i][19];
    if (status === 'Approved') approved++;
    else if (status === 'Pending Review') pending++;
    else if (status === 'Rejected') rejected++;
  }

  return {
    total: total,
    approved: approved,
    pending: pending,
    rejected: rejected
  };
}
```

4. **I-save ang script**:
   - I-click ang **Save** button (disk icon) sa toolbar
   - O kaya, i-press **Ctrl+S** (Windows) o **Cmd+S** (Mac)
   - I-type ang project name: `Sibaguan-KK-Backend`
   - I-click **Rename**

---

### Step 3: Deploy as Web App

1. **I-click ang Deploy button**:
   - Sa taas ng Apps Script editor, i-click ang **Deploy** button
   - I-click ang **New deployment** (o **Manage deployments** kung may existing na)

2. **I-configure ang deployment**:
   - Sa **Type** dropdown, piliin ang **Web app**
   - Sa **Description**, i-type: `KK Profiling API v1.0`
   - Sa **Execute as**, piliin ang **Me (your-email@gmail.com)**
   - Sa **Who has access**, piliin ang **Anyone** (o **Anyone with Google account** para sa mas secure na setup)
   - I-click ang **Deploy**

3. **I-authorize ang permissions**:
   - Mag-a-appear ang dialog na humihingi ng authorization
   - I-click ang **Review Permissions**
   - Piliin ang iyong Google account
   - I-click ang **Advanced** (kung makikita)
   - I-click ang **Go to Sibaguan-KK-Backend (unsafe)**
   - I-check ang lahat ng required permissions:
     - ✅ View and manage your spreadsheets in Google Drive
     - ✅ View and manage data associated with the application
   - I-click ang **Allow**

4. **Tandaan ang Web App URL**:
   - Matapos ma-deploy, mag-a-appear ang dialog na may **Web App URL**
   - Halimbawa: `https://script.google.com/macros/s/AKfycby.../exec`
   - **I-copy ang URL** at i-paste sa isang safe na lugar (text file)
   - I-click ang **Done**

---

### Step 4: Copy the Web App URL

1. **Kung nawala mo ang URL**, maaari mong makuha ito ulit:
   - I-click ang **Deploy** → **Manage deployments**
   - I-click ang **Web app** link
   - I-copy ang URL mula sa dialog

2. **I-verify ang deployment**:
   - Buksan ang Web App URL sa isang bagong browser tab
   - Dapat makita mo ang JSON response:
     ```json
     {"success":true,"data":[],"count":0,"timestamp":"..."}
     ```
   - Kung may existing data, makikita mo ang lahat ng records

---

### Step 5: Update Your HTML Files

1. **Buksan ang `index.html` file** sa isang text editor (VS Code, Notepad++, Sublime Text)

2. **Hanapin ang Google Script URL** (sa bandang taas ng `<script>` tag):
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/YOUR_WEB_APP_URL/exec';
   ```

3. **I-replace ang URL**:
   - I-delete ang `YOUR_WEB_APP_URL` part
   - I-paste ang aktwal na Web App URL mula sa Step 3
   - Halimbawa:
     ```javascript
     const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbyDChU16yDTzWQ-S0J3T2RdkJwNn5W6nvXnZkfk1t-SBApbJvp47C4iQ6STy9XcDDf7/exec';
     ```

4. **Gawin ang pareho sa `admin.html`**:
   - Buksan ang `admin.html`
   - Hanapin ang parehong `GOOGLE_SCRIPT_URL` variable
   - I-replace ang URL sa parehong Web App URL

5. **I-save ang parehong files**

6. **I-test ang connection**:
   - Buksan ang `index.html` sa browser
   - I-fill out ang form at i-submit
   - I-check ang Google Sheet — dapat may bagong row na na-add
   - Buksan ang `admin.html` at i-login
   - Dapat makita ang bagong submission sa table

---

## 📊 Data Flow Architecture

### User Submission Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         USER SUBMISSION FLOW                              │
└─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────┐
  │   User      │
  │  Opens      │
  │ index.html  │
  └──────┬──────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  1. Fill out KK Profiling Form  │
  │     • Personal Information      │
  │     • Contact Information       │
  │     • Education & Work          │
  │     • Skills & Programs         │
  │     • Emergency Contact         │
  │     • ID Picture Upload         │
  │     • Comments                  │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  2. Age Validation (15-30)      │
  │     • Auto-calculate from DOB   │
  │     • Show qualification status │
  │     • Reject if over 30         │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  3. Click SUBMIT                │
  │     • Show loading spinner      │
  │     • Disable submit button     │
  └──────┬──────────────────────────┘
         │
         ├──────────────────────────────────────┐
         │                                      │
         ▼                                      ▼
  ┌─────────────┐                    ┌──────────────────┐
  │  ONLINE     │                    │    OFFLINE       │
  │  MODE       │                    │    MODE          │
  └──────┬──────┘                    └────────┬─────────┘
         │                                    │
         ▼                                    ▼
  ┌──────────────────┐              ┌──────────────────┐
  │ 4a. Send to      │              │ 4b. Save to      │
  │    Google Sheets  │              │    localStorage  │
  │    (POST request) │              │    + Queue       │
  └──────┬───────────┘              └──────┬───────────┘
         │                                  │
         ▼                                  ▼
  ┌──────────────────┐              ┌──────────────────┐
  │ 5a. Google Sheets │              │ 5b. Will sync    │
  │    saves data     │              │    when online   │
  └──────┬───────────┘              └──────────────────┘
         │
         ▼
  ┌──────────────────┐
  │ 6. Save to         │
  │    localStorage    │
  │    (backup)        │
  └──────┬───────────┘
         │
         ▼
  ┌──────────────────┐
  │ 7. Send Email via  │
  │    EmailJS         │
  │    (confirmation)  │
  └──────┬───────────┘
         │
         ▼
  ┌──────────────────┐
  │ 8. Notify Admin   │
  │    via Broadcast  │
  │    Channel        │
  └──────┬───────────┘
         │
         ▼
  ┌──────────────────┐
  │ 9. Show Success   │
  │    Modal + Sound  │
  │    + Voice        │
  └──────────────────┘
```

### Admin Dashboard Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        ADMIN DASHBOARD FLOW                             │
└─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────┐
  │   Admin     │
  │  Opens      │
  │ admin.html  │
  └──────┬──────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  1. Login Screen                │
  │     • Username: admin             │
  │     • Password: admin123        │
  │     • Animated background         │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  2. Dashboard Loads             │
  │     • Real-time clock starts    │
  │     • Stats cards animate       │
  │     • Auto-refresh every 5 sec  │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  3. Fetch Data from Sources      │
  │     (in priority order):         │
  │                                  │
  │     Priority 1: Google Sheets   │
  │     Priority 2: localStorage    │
  │     Priority 3: Empty state     │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │  4. Display Data Table            │
  │     • Pagination (10 per page)    │
  │     • Sortable columns            │
  │     • Search & Filter             │
  │     • Status badges               │
  └──────┬──────────────────────────┘
         │
         ├──────────────────────────────────────┬──────────────────────┐
         │                                      │                      │
         ▼                                      ▼                      ▼
  ┌─────────────┐                    ┌─────────────┐          ┌─────────────┐
  │   VIEW      │                    │   APPROVE   │          │   REJECT    │
  │  ACTION     │                    │   ACTION    │          │   ACTION    │
  └──────┬──────┘                    └──────┬──────┘          └──────┬──────┘
         │                                  │                      │
         ▼                                  ▼                      ▼
  ┌─────────────┐                    ┌─────────────┐          ┌─────────────┐
  │ Show Detail │                    │ Update to   │          │ Update to   │
  │ Modal with  │                    │ "Approved"  │          │ "Rejected"  │
  │ all fields  │                    │             │          │             │
  └─────────────┘                    └──────┬──────┘          └──────┬──────┘
                                            │                      │
                                            ▼                      ▼
                                    ┌─────────────┐          ┌─────────────┐
                                    │ Send Email  │          │ Send Email  │
                                    │ (Approval)  │          │ (Rejection) │
                                    │ via EmailJS  │          │ via EmailJS  │
                                    └──────┬──────┘          └──────┬──────┘
                                           │                      │
                                           ▼                      ▼
                                    ┌─────────────┐          ┌─────────────┐
                                    │ Update      │          │ Update      │
                                    │ Google      │          │ Google      │
                                    │ Sheets      │          │ Sheets      │
                                    └──────┬──────┘          └──────┬──────┘
                                           │                      │
                                           ▼                      ▼
                                    ┌─────────────┐          ┌─────────────┐
                                    │ Show Toast  │          │ Show Toast  │
                                    │ Notification│          │ Notification│
                                    └─────────────┘          └─────────────┘
```

### Real-Time Sync Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      REAL-TIME SYNC ARCHITECTURE                          │
└─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────┐         ┌─────────────────┐
  │   index.html    │         │   admin.html    │
  │   (User Form)   │         │   (Dashboard)   │
  └────────┬────────┘         └────────┬────────┘
           │                           │
           │  ┌─────────────────────┐  │
           └──┤ BroadcastChannel   ├──┘
              │ 'sibaguan_kk_sync'  │
              └─────────────────────┘

           Message Types:
           • new_submission → Notify admin of new data
           • status_update  → Notify user of status change

  ┌─────────────────────────────────────────────────────────┐
  │                    localStorage Events                    │
  │                                                         │
  │  Keys used:                                             │
  │  • 'sibaguan_kk_db'      → All member records          │
  │  • 'kk_last_update'      → Timestamp of last update    │
  │  • 'kk_new_submission'   → Flag for new submissions    │
  │  • 'kk_pending_sync'     → Queue for offline data      │
  │  • 'kk_last_sync'        → Last successful sync time   │
  │                                                         │
  │  Events:                                                │
  │  • storage event → Fires when localStorage changes     │
  │                    in another tab/window                 │
  └─────────────────────────────────────────────────────────┘
```

### Offline Fallback Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     OFFLINE FALLBACK MECHANISM                            │
└─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────┐
  │ User is     │
  │ OFFLINE     │
  └──────┬──────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │ 1. Detect offline status        │
  │    • navigator.onLine === false │
  │    • 'offline' event fires      │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │ 2. Show offline badge            │
  │    • Red notification banner    │
  │    • "Will sync when online"    │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │ 3. Save to localStorage         │
  │    • Add to 'sibaguan_kk_db'    │
  │    • Add to 'kk_pending_sync'   │
  │    • Set 'kk_last_update'       │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │ 4. User comes back ONLINE       │
  │    • 'online' event fires       │
  │    • Check pending sync queue   │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │ 5. Sync pending data            │
  │    • Loop through queue         │
  │    • POST each to Google Sheets │
  │    • Remove from queue if OK    │
  │    • Keep in queue if failed    │
  └──────┬──────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────┐
  │ 6. Show sync status             │
  │    • "X records synced!"        │
  │    • Or "X still pending"       │
  └─────────────────────────────────┘
```

---

## 🔐 Security Features

### Frontend Security

| Feature | Implementation | Description |
|---------|---------------|-------------|
| **Age Validation** | JavaScript calculation | Auto-calculates age from DOB, rejects if not 15-30 |
| **Input Sanitization** | `escapeHtml()` function | Prevents XSS attacks in table rendering |
| **Admin Authentication** | Hardcoded credentials | Username: `admin`, Password: `admin123` |
| **CSRF Protection** | N/A (stateless) | No session cookies, uses localStorage |
| **Data Encryption** | Base64 (images only) | ID pictures encoded as base64 |

### Recommended Production Security

⚠️ **IMPORTANT:** Para sa production deployment, i-implement ang mga sumusunod:

1. **Server-side Authentication**
   - Gumamit ng JWT (JSON Web Tokens)
   - Implement OAuth 2.0 o Firebase Auth
   - Hash passwords with bcrypt/Argon2

2. **HTTPS Only**
   - Force HTTPS sa lahat ng connections
   - Use HSTS headers

3. **Rate Limiting**
   - Limit submissions per IP address
   - Prevent spam and abuse

4. **Data Validation**
   - Server-side validation (not just client-side)
   - Sanitize all inputs

5. **CORS Restriction**
   - Restrict `Access-Control-Allow-Origin` sa specific domain
   - Huwag gamitin ang `*` sa production

6. **API Key Management**
   - Huwag i-hardcode ang API keys
   - Gumamit ng environment variables
   - Rotate keys regularly

---

## 📧 EmailJS Integration

### Setup Instructions

1. **Gumawa ng EmailJS account**:
   - Pumunta sa [EmailJS website](https://www.emailjs.com/)
   - I-click ang **Get Started** o **Sign Up**
   - Gumamit ng Google account o email para mag-register
   - I-verify ang email address

2. **Gumawa ng Email Service**:
   - I-log in sa EmailJS dashboard
   - I-click ang **Email Services** sa sidebar
   - I-click ang **Add New Service**
   - Piliin ang **Gmail** (recommended) o ibang email provider
   - I-connect ang iyong Gmail account
   - I-copy ang **Service ID** (hal: `service_djne9ym`)

3. **Gumawa ng Email Template**:
   - I-click ang **Email Templates** sa sidebar
   - I-click ang **Create New Template**
   - I-design ang template gamit ang HTML/CSS
   - I-include ang mga variables:
     ```html
     <h2>Hello {{to_name}}!</h2>
     <p>{{message}}</p>
     <p>Status: {{status_icon}} {{status_text}}</p>
     ```
   - I-save ang template
   - I-copy ang **Template ID** (hal: `template_q5v9o8w`)

4. **Kunin ang Public Key**:
   - I-click ang **Account** sa sidebar
   - Hanapin ang **API Keys** section
   - I-copy ang **Public Key** (hal: `S3_XQI5mfn8MMdGhM`)

5. **I-update ang HTML files**:
   - Sa `index.html` at `admin.html`, hanapin ang:
     ```javascript
     emailjs.init("S3_XQI5mfn8MMdGhM");
     ```
   - I-replace ang Public Key kung kailangan
   - Sa `sendConfirmationEmail()`, `sendApprovalEmail()`, at `sendRejectionEmail()` functions, i-update ang:
     - `service_djne9ym` → iyong Service ID
     - `template_q5v9o8w` → iyong Template ID

6. **I-test ang email**:
   - I-submit ang form gamit ang valid email address
   - I-check ang inbox (at spam folder)
   - Dapat makatanggap ng confirmation email

### Email Types

| Email Type | Trigger | Recipient | Content |
|-----------|---------|-----------|---------|
| **Confirmation** | Form submission | User's email | Thank you + pending status |
| **Approval** | Admin clicks "Approve" | User's email | Congratulations + approved status |
| **Rejection** | Admin clicks "Reject" | User's email | Sorry + rejected status |

---

## 🎵 Voice & Sound Effects

### Audio Engine Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      AUDIO ENGINE ARCHITECTURE                            │
└─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────┐
  │  AudioEngine    │
  │  (Web Audio API)│
  └────────┬────────┘
           │
           ├──────────────────────────────────────────────┐
           │                                              │
           ▼                                              ▼
  ┌─────────────────┐                           ┌─────────────────┐
  │  Sound Effects  │                           │  VoiceEngine    │
  │                 │                           │  (SpeechSynthesis)│
  │ • playTone()    │                           │                 │
  │ • playChord()   │                           │ • speak()       │
  │ • playSuccess() │                           │ • welcome()     │
  │ • playError()   │                           │ • success()     │
  │ • playClick()   │                           │ • reject()      │
  │ • playHover()   │                           │ • fieldFocus()  │
  │ • playType()    │                           │                 │
  │ • playSubmit()  │                           │                 │
  │ • playWelcome() │                          │                 │
  └─────────────────┘                           └─────────────────┘
```

### Sound Triggers

| Event | Sound | Description |
|-------|-------|-------------|
| **Page Load** | Welcome melody | Ascending C major chord |
| **Form Focus** | Focus tone | 880Hz sine wave |
| **Typing** | Type sound | Random 600-800Hz |
| **Radio/Checkbox click** | Click sound | 800Hz short beep |
| **Hover** | Hover sound | 1200Hz very subtle |
| **Submit button** | Submit sound | C-E-G ascending |
| **Success modal** | Success chord | C-E-G-C + sparkle |
| **Reject modal** | Error sound | Descending A-F-D |
| **Age validation OK** | Chord | C-E major |
| **Age validation fail** | Error | Descending tones |
| **Photo upload** | Click | Standard click |
| **Online** | Chord | C-E-G ascending |
| **Offline** | Error | Descending tones |
| **Minute tick** | Tick | 1200Hz subtle |
| **Scroll** | Whoosh | 400Hz short |

### Voice (Text-to-Speech) Triggers

| Event | Voice Text | Language |
|-------|-----------|----------|
| **Welcome** | "Welcome to Barangay Sibaguan KK Profiling System..." | English |
| **Success** | "Congratulations [name]! Your KK Profiling has been successfully submitted..." | English |
| **Rejection** | "We apologize, but your age does not meet the requirements..." | English |
| **Field Focus** | "Please enter your [field name]" | English |

### Initialization

```javascript
// Audio initializes on FIRST user interaction (click or touch)
// This is required by browsers (autoplay policy)

document.addEventListener('click', initAudio, { once: true });
document.addEventListener('touchstart', initAudio, { once: true });

function initAudio() {
  AudioEngine.init();        // Initialize Web Audio API
  VoiceEngine.init();        // Initialize SpeechSynthesis

  // Play welcome sounds after short delay
  setTimeout(() => {
    AudioEngine.playWelcome();
    VoiceEngine.welcome();
  }, 800);
}
```

---

## 🎨 UI/UX Features

### Animations & Effects

| Feature | File | Description |
|---------|------|-------------|
| **Floating Circles** | Both | Background animated circles |
| **Particle Effects** | index.html | Floating gold particles |
| **Wave Shapes** | Both | Top/bottom wave decorations |
| **Logo Pulse** | Both | Pulsing logo animation |
| **Slide Up** | Both | Cards sliding up on load |
| **Fade In** | Both | Content fading in |
| **Slide In Left** | admin.html | Table rows sliding in |
| **Scale In** | Both | Modals scaling in |
| **Shake** | Both | Error shake animation |
| **Bounce** | Both | Success bounce animation |
| **Pulse Dot** | admin.html | Real-time indicator |
| **Glow Effect** | Both | Admin badge glow |
| **Shimmer** | admin.html | Button hover shimmer |
| **Footer Waves** | Both | Animated SVG wave footer |
| **Footer Particles** | Both | Floating particles in footer |
| **Footer Glow** | Both | Radial gradient glow |

### Color Scheme

| Element | Color | Hex Code |
|---------|-------|----------|
| **Primary** | Philippine Blue | `#0033A0` |
| **Secondary** | Gold | `#FFD700` |
| **Success** | Green | `#00C853` |
| **Warning** | Orange | `#E65100` |
| **Error** | Red | `#e74c3c` |
| **Background** | Light Gray | `#f0f2f5` |
| **Card** | White | `#ffffff` |

### Typography

- **Font Family:** Poppins (Google Fonts)
- **Weights Used:** 300, 400, 500, 600, 700, 800, 900
- **Primary Text:** Dark gray `#333`
- **Secondary Text:** Medium gray `#666`
- **Muted Text:** Light gray `#999`

---

## 📱 Responsive Design

### Breakpoints

| Breakpoint | Width | Adjustments |
|-----------|-------|-------------|
| **Mobile** | < 600px | Single column, smaller fonts, stacked buttons |
| **Tablet** | 600-768px | 2-column grid, medium fonts |
| **Desktop** | > 768px | Full layout, large fonts, side-by-side |

### Mobile Optimizations

- ✅ Stack form rows vertically
- ✅ Reduce logo size (100px → 70px)
- ✅ Reduce title sizes
- ✅ Full-width buttons
- ✅ Touch-friendly tap targets (min 44px)
- ✅ Horizontal scroll for tables
- ✅ Collapsed header layout

---

## 🗂️ Database Schema

### Google Sheets Schema

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    GOOGLE SHEETS COLUMN MAP                               │
└─────────────────────────────────────────────────────────────────────────┘

Row 1: HEADERS
┌─────┬───────────┬──────────┬─────┬──────────┬────────┬─────────────┬───────┐
│  A  │     B     │    C     │  D  │    E     │   F    │      G      │   H   │
├─────┼───────────┼──────────┼─────┼──────────┼────────┼─────────────┼───────┤
│ ID  │ Timestamp │ FullName │ Age │ BirthDate│ Gender │ CivilStatus │ Purok │
└─────┴───────────┴──────────┴─────┴──────────┴────────┴─────────────┴───────┘

┌───────┬─────────┬───────────┬────────────┬──────────┬─────────┬──────────┐
│   I   │    J    │     K     │     L      │    M     │    N    │    O     │
├───────┼─────────┼───────────┼────────────┼──────────┼─────────┼──────────┤
│Contact│  Email  │ Education │ Employment │  Skills  │ KKBefore│ Programs │
└───────┴─────────┴───────────┴────────────┴──────────┴─────────┴──────────┘

┌───────────────┬─────────────────┬──────────────────┬─────────┬────────┬─────────────┬─────────────┬─────────────┐
│       P       │        Q        │        R         │    S    │   T    │      U      │      V      │      W      │
├───────────────┼─────────────────┼──────────────────┼─────────┼────────┼─────────────┼─────────────┼─────────────┤
│ EmergencyName │ EmergencyContact│ EmergencyRelation│ Comments│ Status │ FormattedDate│ ApprovedDate│ IDPictureURL│
└───────────────┴─────────────────┴──────────────────┴─────────┴────────┴─────────────┴─────────────┴─────────────┘
```

### localStorage Schema

```javascript
// Key: 'sibaguan_kk_db'
// Value: JSON array of member objects

[
  {
    "id": "1712345678901",
    "timestamp": "2026-05-04T10:00:00.000Z",
    "formattedDate": "Mayo 4, 2026, 10:00:00 AM",
    "fullName": "Juan Dela Cruz",
    "age": 22,
    "birthDate": "2004-03-15",
    "gender": "Male",
    "civilStatus": "Single",
    "purok": "Purok 3",
    "contactNumber": "09123456789",
    "email": "juan@example.com",
    "education": "College Graduate",
    "employment": "Employed",
    "skills": ["Sports", "Leadership"],
    "kkBefore": "No",
    "programs": ["Sports", "Education"],
    "emergencyName": "Maria Dela Cruz",
    "emergencyContact": "09987654321",
    "emergencyRelation": "Mother",
    "idPicture": "data:image/jpeg;base64,/9j/4AAQ...",
    "comments": "Excited to join!",
    "status": "Pending Review"
  }
]
```

---

## 🔧 Troubleshooting

### Common Issues & Solutions

#### Issue 1: "Walang data sa admin dashboard"

**Symptoms:**
- Admin dashboard shows "Walang Records"
- Table is empty

**Solutions:**
1. I-check ang Google Script URL sa parehong files
2. I-verify na deployed ang Web App
3. I-check ang browser console para sa errors (F12 → Console)
4. I-try ang localStorage mode (disconnect internet)
5. I-refresh ang page at i-try ulit

#### Issue 2: "Hindi nagse-send ang email"

**Symptoms:**
- Success modal shows pero walang email
- EmailJS error sa console

**Solutions:**
1. I-verify ang EmailJS Public Key
2. I-check ang Service ID at Template ID
3. I-verify na verified ang email sa EmailJS
4. I-check ang spam folder
5. I-try ang ibang email provider (Gmail → Outlook)

#### Issue 3: "404 Not Found sa Google Script"

**Symptoms:**
- Network error sa console
- HTTP 404 status

**Solutions:**
1. I-verify na deployed ang Web App (Deploy → Manage deployments)
2. I-check kung tama ang URL (hindi may extra spaces)
3. I-redeploy ang Web App (Deploy → New deployment)
4. I-check ang Google Apps Script permissions

#### Issue 4: "CORS Error"

**Symptoms:**
- Console shows "CORS policy" error
- "No 'Access-Control-Allow-Origin' header"

**Solutions:**
1. I-verify ang CORS headers sa Apps Script
2. I-check na tama ang `doOptions()` function
3. I-try ang `no-cors` mode sa fetch requests
4. I-redeploy ang Web App

#### Issue 5: "Hindi nag-a-auto refresh ang admin"

**Symptoms:**
- Bagong submission pero hindi lumalabas sa admin
- Kailangan i-refresh ang page

**Solutions:**
1. I-check ang BroadcastChannel support (Chrome/Edge/Firefox OK)
2. I-verify ang localStorage events
3. I-check ang auto-refresh interval (5 seconds)
4. I-refresh manually (F5)

#### Issue 6: "Masyadong malaki ang ID picture"

**Symptoms:**
- Form submission fails
- "File too large" error

**Solutions:**
1. I-compress ang image bago i-upload
2. I-resize ang image sa Photoshop/GIMP
3. I-use online image compressor (tinypng.com)
4. I-check ang 5MB limit sa code

#### Issue 7: "Hindi gumagana ang sound/voice"

**Symptoms:**
- Walang sound effects
- Walang text-to-speech

**Solutions:**
1. I-click anywhere sa page (browser autoplay policy)
2. I-check ang Web Audio API support
3. I-verify ang SpeechSynthesis support
4. I-check ang volume settings
5. I-try ang ibang browser

---

## 📞 Support

### Developer Contact

| Detail | Information |
|--------|-------------|
| **Developer** | Roniel Nyke Gonzales |
| **Company** | Lambunao Web Developer |
| **Email** | ronielnyke@gmail.com |
| **Year** | 2026 |

### Resources

- 📖 [Google Apps Script Documentation](https://developers.google.com/apps-script)
- 📖 [EmailJS Documentation](https://www.emailjs.com/docs/)
- 📖 [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- 📖 [BroadcastChannel API](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API)
- 📖 [SpeechSynthesis API](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis)

### License

© 2026 **Barangay Sibaguan** — KK Profiling System. All rights reserved.

Developed by **Roniel Nyke Gonzales** | **Lambunao Web Developer**

---

## 🎉 Quick Start Checklist

- [ ] 1. Create Google Sheet with correct headers
- [ ] 2. Open Apps Script editor
- [ ] 3. Paste the complete Apps Script code
- [ ] 4. Save the project
- [ ] 5. Deploy as Web App
- [ ] 6. Authorize permissions
- [ ] 7. Copy the Web App URL
- [ ] 8. Update `GOOGLE_SCRIPT_URL` in `index.html`
- [ ] 9. Update `GOOGLE_SCRIPT_URL` in `admin.html`
- [ ] 10. Set up EmailJS account
- [ ] 11. Create email service and template
- [ ] 12. Update EmailJS credentials in both files
- [ ] 13. Test form submission
- [ ] 14. Verify data in Google Sheet
- [ ] 15. Test admin dashboard
- [ ] 16. Test approve/reject functionality
- [ ] 17. Test email notifications
- [ ] 18. Test offline mode
- [ ] 19. Test responsive design on mobile
- [ ] 20. 🎉 System ready for production!

---


---

## 🎙️ Enhanced Voice & Sound System (NEW — index.html v2.0)

> **Added in May 2026** — Pinahusay na voice greeting at sound effects para sa mas magandang user experience.

### 🆕 New Features Overview

| Feature | Description | Trigger |
|---------|-------------|---------|
| **👋 Smart Welcome Banner** | Visual greeting banner with time-based message | Page load + first click |
| **🗣️ Voice Greeting** | Premium natural voice says welcome message | Page load + first click |
| **🎵 Welcome Music** | Beautiful C major arpeggio with harmonics | Page load + first click |
| **📛 Name Announcement** | Voice says the submitter's actual name | Form submission success |
| **🎉 Success Fanfare** | Triumphant celebration music | Form submission success |
| **💎 Premium Voice Selection** | Auto-selects best available TTS voice | System initialization |

---

### 👋 Smart Welcome Banner

Pagpasok ng user sa website at nag-click kahit saan, lalabas ang banner sa taas ng screen:

```
┌─────────────────────────────────────────────────────────────┐
│  ☀️ Magandang Umaga! Good Morning! Welcome to Barangay       │
│     Sibaguan KK Profiling System!                            │
└─────────────────────────────────────────────────────────────┘
```

**Time-Based Greetings:**

| Time Range | Filipino | English | Icon |
|------------|----------|---------|------|
| 5:00 AM – 11:59 AM | Magandang Umaga! | Good Morning! | ☀️ |
| 12:00 PM – 4:59 PM | Magandang Hapon! | Good Afternoon! | 🌤️ |
| 5:00 PM – 4:59 AM | Magandang Gabi! | Good Evening! | 🌙 |

**Banner Behavior:**
- Slides down from top with **cubic-bezier bounce animation**
- Auto-hides after **5 seconds**
- Gold border accent matching the theme
- Responsive on mobile devices

---

### 🗣️ Premium Voice Greeting System

#### Voice Selection Priority

The system automatically selects the **best available Text-to-Speech voice** from the browser:

| Priority | Voice Name | Quality | Platform |
|----------|-----------|---------|----------|
| 1 | Microsoft Michelle Online (Natural) | ⭐⭐⭐⭐⭐ Premium | Windows/Edge |
| 2 | Microsoft Sonia Online (Natural) | ⭐⭐⭐⭐⭐ Premium | Windows/Edge |
| 3 | Microsoft Emma Online (Natural) | ⭐⭐⭐⭐⭐ Premium | Windows/Edge |
| 4 | Microsoft Jenny Online (Natural) | ⭐⭐⭐⭐⭐ Premium | Windows/Edge |
| 5 | Microsoft Ana Online (Natural) | ⭐⭐⭐⭐⭐ Premium | Windows/Edge |
| 6 | Google US English | ⭐⭐⭐⭐ High | Chrome |
| 7 | Google UK English Female | ⭐⭐⭐⭐ High | Chrome |
| 8 | Samantha (Apple) | ⭐⭐⭐⭐ High | macOS/Safari |
| 9 | Victoria (Apple) | ⭐⭐⭐⭐ High | macOS/Safari |
| 10 | Karen (Apple) | ⭐⭐⭐⭐ High | macOS/Safari |

> 💡 **Tip:** Para sa pinakamagandang boses, gamitin ang **Microsoft Edge browser** sa Windows. Mayroon itong "Natural" voices na halos parang totoong tao na magsalita.

#### Voice Fine-Tuning Settings

```javascript
utterance.rate = 0.92;    // Slightly slower for clarity
utterance.pitch = 1.05;   // Slightly higher for warmth
utterance.volume = 0.95;  // Near maximum volume
utterance.lang = 'en-US'; // US English accent
```

#### Welcome Voice Script

**Pagpasok sa site (depende sa oras):**

> *"Magandang Umaga! Good morning! Welcome to Barangay Sibaguan KK Profiling System. Please fill out the form with your accurate information. Your data is secure and protected."*

> *"Magandang Hapon! Good afternoon! Welcome to Barangay Sibaguan KK Profiling System. Please fill out the form with your accurate information. Your data is secure and protected."*

> *"Magandang Gabi! Good evening! Welcome to Barangay Sibaguan KK Profiling System. Please fill out the form with your accurate information. Your data is secure and protected."*

---

### 🎵 Enhanced Audio Engine

#### Welcome Music (C Major Arpeggio)

Pagpasok ng user, tumutugtog ang magandang musika:

```
Notes: C4 → E4 → G4 → C5 → E5 → G5 → C6
       (261.63Hz → 329.63Hz → 392.00Hz → 523.25Hz → 659.25Hz → 783.99Hz → 1046.50Hz)

Style: Ascending arpeggio with harmonic overtones
Duration: ~1.5 seconds
Effect: Crystal-like, uplifting, welcoming
```

#### Success Fanfare (Name Announcement)

Pag na-submit ang form at approved ang age:

```
Chord 1: C-E-G-C (523.25, 659.25, 783.99, 1046.50 Hz)
Chord 2: E-G-C-E (659.25, 783.99, 1046.50, 1318.51 Hz)
Sparkle: G-B-D (1567.98, 1975.53, 2349.32 Hz)

Style: Triumphant, celebratory
Duration: ~2 seconds
Effect: Parang graduation ceremony!
```

#### Personalized Name Announcement

Pag na-submit ang form, sinasabi ng boses ang **totoong pangalan** ng nag-submit:

> *"Congratulations Juan Dela Cruz! Your KK Profiling has been successfully submitted. A confirmation email has been sent to your email address. Thank you for participating in the Katipunan ng Kabataan program."*

**Paano kinukuha ang pangalan:**
```javascript
const firstName = document.getElementById('firstName').value.trim();
const lastName = document.getElementById('lastName').value.trim();
const fullName = firstName + (lastName ? ' ' + lastName : '');
```

---

### 🎧 Complete Sound Event Map

| Event | Sound | Voice | Description |
|-------|-------|-------|-------------|
| **Page Load** | Welcome music + chime | Time-based greeting | Full welcome sequence |
| **Field Focus** | 990Hz soft tone | — | Input field focused |
| **Typing** | 600-900Hz random | — | Each keystroke |
| **Radio/Checkbox Click** | 880Hz click | — | Option selected |
| **Hover** | 1320Hz subtle | — | Mouse over element |
| **Age Valid (15-30)** | C-E major chord | — | Happy confirmation |
| **Age Invalid** | Descending empathy | — | Gentle rejection tone |
| **Submit Button** | C-E-G ascending | — | Submit initiated |
| **Form Success** | Full fanfare | Name announcement | Celebration! |
| **Form Rejected** | Soft descending | Rejection message | Empathetic |
| **Photo Upload** | Clean click | — | Image selected |
| **Online** | C-E-G bright chord | — | Connection restored |
| **Offline** | Gentle warning | — | Connection lost |
| **Minute Tick** | 1200Hz subtle | — | Every minute |
| **Scroll** | 400Hz whoosh | — | Page scroll |

---

### 🔊 Audio Initialization

> ⚠️ **IMPORTANT:** Dahil sa browser autoplay policy, kailangan ng **user interaction** (click o touch) bago mag-play ang audio.

```javascript
// Initialize on first user interaction
document.addEventListener('click', initAudio, { once: true });
document.addEventListener('touchstart', initAudio, { once: true });

async function initAudio() {
    AudioEngine.init();        // Web Audio API
    VoiceEngine.init();        // Speech Synthesis

    // Show welcome banner
    showWelcomeBanner();

    // Play welcome sequence
    setTimeout(async () => {
        AudioEngine.playWelcomeMusic();
        await VoiceEngine.greetingByTime();
    }, 600);
}
```

**Supported Browsers:**
- ✅ Chrome 60+
- ✅ Edge 79+ (Recommended — best voices)
- ✅ Firefox 60+
- ✅ Safari 14+
- ✅ Opera 47+
- ✅ Samsung Internet 8+

---

### 🛠️ Technical Implementation

#### Enhanced Audio Engine Structure

```
┌─────────────────────────────────────────────────────────────┐
│                    ENHANCED AUDIO ENGINE                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌───────────────┐      ┌─────────────────┐                │
│  │ AudioEngine   │      │  VoiceEngine    │                │
│  │ (Web Audio)   │      │ (SpeechSynth)   │                │
│  ├───────────────┤      ├─────────────────┤                │
│  │ • playTone()  │      │ • speak()       │                │
│  │ • playChord() │      │ • welcome()     │                │
│  │ • playArpeg.  │◄────►│ • success()     │                │
│  │ • playWelcome │      │ • reject()      │                │
│  │ • playSuccess │      │ • greetingByTime│                │
│  │ • playReject  │      │ • fieldFocus()  │                │
│  │ • playClick   │      │                 │                │
│  │ • playHover   │      │ Voice Priority: │                │
│  │ • playType    │      │ 1. Microsoft    │                │
│  │ • playFocus   │      │    Natural      │                │
│  │ • playSubmit  │      │ 2. Google       │                │
│  │ • playGreet   │      │ 3. Apple        │                │
│  │   Chime       │      │ 4. Samsung      │                │
│  └───────────────┘      └─────────────────┘                │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              WELCOME BANNER SYSTEM                   │   │
│  │  • Time-based greeting text                          │   │
│  • Slide-down animation (cubic-bezier)               │   │
│  │  • Auto-hide after 5 seconds                         │   │
│  │  • Responsive design                                 │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

### 📝 Updated Quick Start Checklist (with Voice Features)

- [ ] 1. Create Google Sheet with correct headers
- [ ] 2. Open Apps Script editor
- [ ] 3. Paste the complete Apps Script code
- [ ] 4. Save the project
- [ ] 5. Deploy as Web App
- [ ] 6. Authorize permissions
- [ ] 7. Copy the Web App URL
- [ ] 8. Update `GOOGLE_SCRIPT_URL` in `index.html`
- [ ] 9. Update `GOOGLE_SCRIPT_URL` in `admin.html`
- [ ] 10. Set up EmailJS account
- [ ] 11. Create email service and template
- [ ] 12. Update EmailJS credentials in both files
- [ ] 13. Test form submission
- [ ] 14. Verify data in Google Sheet
- [ ] 15. Test admin dashboard
- [ ] 16. Test approve/reject functionality
- [ ] 17. Test email notifications
- [ ] 18. Test offline mode
- [ ] 19. Test responsive design on mobile
- [ ] 20. **🎙️ Test voice greeting — click page and listen**
- [ ] 21. **🎵 Test welcome music — should play on first click**
- [ ] 22. **📛 Test name announcement — submit form with name**
- [ ] 23. **🎧 Test all UI sounds — click, hover, type, focus**
- [ ] 24. **🔊 Test age validation sounds — valid and invalid ages**
- [ ] 25. **📶 Test online/offline sounds — toggle connection**
- [ ] 26. 🎉 System ready for production!

---

### 🔄 Version History

| Version | Date | Changes |
|---------|------|---------|
| **v1.0** | March 2026 | Initial release — basic form, admin dashboard, Google Sheets sync |
| **v2.0** | May 2026 | Added premium voice greeting, welcome banner, name announcement, enhanced sound effects |

---
**Maraming salamat sa paggamit ng Barangay Sibaguan KK Profiling System!**

*"Para sa mga kabataan, para sa kinabukasan."*
