# 🚀 IDB WebBridge v0.1.4

### Printing Enhancements • Interface Monitoring • Order Chit History

**Version 0.1.4** introduces enhanced printing diagnostics, improved interface monitoring, and a new **Order Chit History** feature with optional PDF saving and previews.

This release focuses on making printing issues easier to troubleshoot, improving system visibility, and helping cashiers manage order chit printing more effectively.

---

## ✨ What's New

### 🖨️ 1. Enhanced Interface Printing

- **IDBScript PDF Printing (Beta)** — Added a new PDF printing engine as an alternative to Ghostscript.
- **Test Printing** — Added interface test printing to verify printer and print engine configurations.
- **Improved Error Handling** — Clearer messages for missing printers, PDF files, and configuration issues.
- **Detailed Print Responses** — `PrintOrderChit` now provides individual chit submission status, error reason, order ID, target printer, and remote PDF URL.
- **Updated Windows Interface** — The Windows build now rebuilds and packages the latest `IDBPOSInterface.exe` from the VB.NET source.

### 📋 2. New Order Chit History

Introducing **Order Chit History**, a new feature for tracking and reviewing order chit printing activity.

**Key Features:**
- ✅ **Submitted** — Print job accepted by the print engine.
- ❌ **Failed** — PDF download or print submission failed.
- ⚠️ **Unconfirmed** — Print result could not be reliably determined.
- Search history by order ID or printer.
- Filter records by date and printing status.
- Export all history records in JSONL format.
- Clear history records and saved PDFs with confirmation.
- History sidebar automatically appears after the first record.

> **Note:** Enable **Record Order Log** in Settings to activate this feature. It is disabled by default.

### 📄 3. Save & Preview Order Chit PDFs

- **Download & Save Order Chit** — Optionally save copies of order chit PDFs to `Downloads/IDBWebridge`.
- **No Duplicate Downloads** — Reuses the PDF already downloaded by the printing interface.
- **PDF Preview** — Open saved order chits in a dedicated viewing window.
- **Page Navigation & Zoom** — Navigate multiple pages and adjust PDF zoom.
- **Independent Saving** — A local PDF saving failure does not stop the printing attempt.

### 🩺 4. Interface Health & Monitoring

- Added a dedicated interface health-check response.
- Improved interface process and port monitoring.
- Enhanced automatic interface recovery behavior.
- Added interface logs directly within IDB WebBridge.
- Improved connection diagnostics and service error reporting.

### 💻 5. Cashier Interface Improvements

- Improved interface connection status indicators.
- Refined network connectivity indicators.
- Enhanced fullscreen toolbar controls.
- Clearer printing, configuration, and settings error messages.
- Improved printing operation feedback.

---

## 🔍 Printing Status & Error Reference

Improved printing feedback makes troubleshooting easier and helps prevent accidental duplicate print jobs.

### ✅ Sent to Printer / Submitted

The print engine successfully accepted the job.

> **Note:** Physical paper output is not guaranteed.

### ❌ Failed: KO — Not Found

The remote server could not locate the requested order chit PDF.

**Recommended Action:** Verify the order ID, company/project codes, and remote PDF URL.

### ❌ Failed: KO …

The interface reported a PDF download or print submission failure.

**Recommended Action:** Review the detailed error message and affected printer.

### ⚠️ Not Able To Connect IDBPOSIF Server!

Web POS could not receive a response from the local printing interface.

**Recommended Action:** Check the interface connection and service status. Verify the printer before retrying, as the print result may still be unknown.

### ⏱️ No Confirmation Within 60 Seconds

Web POS did not receive a reliable confirmation within the timeout period. The order chit may still print.

**Recommended Action:** Check the printer and Order Chit History before retrying to avoid duplicate printing.

### 📄 Could Not Save Order Chit Copy

The optional local PDF saving operation failed.

**Recommended Action:** Check `Downloads/IDBWebridge` and interface logs. The interface still attempts to print using the downloaded PDF.

---

## ⚠️ Important Printing Behavior

**✅ Submitted ≠ Physically Printed**

The printing engine accepted the job, but physical paper output is not confirmed.

**❌ Remote PDF Download Failed**

The affected order chit cannot be printed because the source PDF was not retrieved.

**📄 Local PDF Saving Failed**

The printing attempt continues independently, even if the optional PDF copy could not be saved.

**⚠️ Unconfirmed Print Status**

Some direct browser requests may appear as Unconfirmed when the HTTP response does not reliably indicate the result.

**🔁 Avoid Duplicate Printing**

If a request times out or returns an unknown result, check the printer and Order Chit History before attempting to print again.

---

## ⚙️ Installation & Upgrade Notes

### 🪟 Windows Interface

The updated Windows interface requires the following tools to build the installer:

- Visual Studio with **.NET desktop development** tools.
- **.NET Framework 4.8 Targeting Pack**.
- Updated `IDBPOSInterface.exe`, rebuilt from the VB.NET source.

For complete build and packaging instructions, refer to:

`WINDOWS_BUILD_GUIDE.md`

### 🌐 Web POS Integration

> **Important:** Enhanced multi-chit printing alerts and updated timeout handling require a **separate Web POS deployment**.

- Updating IDB WebBridge alone does not automatically update existing Web POS pages.
- Existing Web POS pages will continue using their previous alert and timeout behavior until updated.
- The updated Web POS integration provides clearer multi-chit responses and timeout handling.

For integration instructions, sample JSONP responses, and alert behavior, refer to:

`PRINT_ORDER_CHIT_WEB_POS_HANDOFF.md`

---

## 🧪 Recommended Testing

Please verify the following features when testing **v0.1.4**.

### 🖨️ Printing
- Test PDF printing using **Ghostscript**.
- Test the new **IDBScript PDF Printing (Beta)** engine.
- Verify interface test printing.
- Check printing errors and status messages.

### 📋 Order Chit History
- Enable **Record Order Log** in Settings.
- Print order chits and verify history records.
- Verify **Submitted**, **Failed**, and **Unconfirmed** statuses.
- Test search, filtering, export, and clear history functionality.

### 📄 PDF Saving & Preview
- Enable **Download & Save Order Chit**.
- Verify PDFs are saved to the correct folder.
- Open saved PDFs from History.
- Test page navigation and zoom controls.

### 🩺 Interface Monitoring
- Verify interface connection and health status.
- Check interface logs.
- Test interface recovery behavior when the service becomes unavailable.

### 💻 User Interface
- Verify network and connection status indicators.
- Test fullscreen toolbar controls.
- Check printing and configuration error notifications.

---

## 📌 Additional Notes

- **Order Chit History** is optional and disabled by default.
- **Download & Save Order Chit** is optional.
- **IDBScript PDF Printing** is currently a Beta feature.
- A **Submitted** status confirms print job acceptance, not physical paper output.
- Updated multi-chit Web POS alerts require a separate deployment.
- Interface logs and Order Chit History can help investigate printing issues.

---

### 🚀 IDB WebBridge v0.1.4

**Better Printing Diagnostics • Smarter Interface Monitoring • Easier Order Chit Management**

*Thank you for testing IDB WebBridge! Please report any bugs, printing issues, or unexpected behavior to the development team.*
