---
name: skill-google-services
description: Integration with Google Sheets, Drive, and Apps Script using Python (gspread) and batch operations.
---

# Google Services Integrator

This guide focuses on high-performance integration with Google Sheets and Automation.

## 1. Google Sheets with gspread

### Connection & Auth
- Use **Service Account** keys (`.json`) for server-side scripts.
- Secure the key file (avoid Git) or use environment variables for key content.

### Reading Data
- Use `get_all_values()` for small sheets.
- Use `get_all_records()` to get data as a list of dictionaries (keys are headers).

### Writing Data (Performance)
- **Avoid single cell updates**: Loop + `update_cell` is extremely slow and hits API limits.
- **Batch Updates**: Use `update()` with a list of lists or `update_cells()` with a range.
- **Append**: Use `append_row()` or `append_rows()` for adding logs or new entries.

---

## 2. Google Apps Script (GAS)

Use GAS for tasks that need to run *inside* the Google environment.

### Deployment & Triggering
- Deploy as **Web App** with `doGet(e)` or `doPost(e)` to create a custom API.
- Use **installable triggers** for time-based or event-based execution.

### Patterns
- **Discovery Mode**: Automatically find headers or data ranges if sheet structure is dynamic.
- **CDC (Change Data Capture)**: Mark rows as "synced" or use hashes to track changes between Sheet and DB.

---

## 3. Quotas & Limits

- **Rate Limits**: 100 requests per 100 seconds per user (approx).
- **Timeouts**: Web App executions have a strict 6-minute limit.
- **Memory**: GAS has memory limits (around 1GB); for large data, process in chunks or move to Python.

## 4. Best Practices

- **Header Management**: Keep headers in the first row. Don't use merged cells in data ranges.
- **Formatting**: Use conditional formatting in Sheets for status visualization.
- **Backup**: Regularly snapshot important sheets before large batch operations.
