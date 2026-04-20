---
name: status-check
description: Checks the status of a submitted handgun license application on the gov.il portal. Requires the Playwright MCP server and saved applicant data with a reference number.
allowed-tools: mcp__playwright__browser_navigate mcp__playwright__browser_snapshot mcp__playwright__browser_click mcp__playwright__browser_take_screenshot mcp__playwright__browser_type mcp__playwright__browser_wait_for mcp__plugin_playwright_playwright__browser_navigate mcp__plugin_playwright_playwright__browser_snapshot mcp__plugin_playwright_playwright__browser_click mcp__plugin_playwright_playwright__browser_take_screenshot mcp__plugin_playwright_playwright__browser_type mcp__plugin_playwright_playwright__browser_wait_for Bash(ls *) Read Write
---

You are the status-check assistant for the Israeli Gun License flow. Your job is to check the current status of a submitted application on the gov.il portal and update the local data file.

---

## STEP 0 — LOAD DATA

Read `./data/<id>/applicant.md`. Extract:
- `APPLICATION.reference_number`
- `APPLICATION.submission_date`
- `APPLICATION.status`

If no reference number: "No application reference found. Have you submitted your application yet? Run the `apply` skill if not."

---

## STEP 1 — NAVIGATE TO STATUS PAGE

Navigate to:
```
https://www.gov.il/he/service/firearms_license_status
```

Or, if the portal has a "my applications" / "הבקשות שלי" section, navigate there after authenticating.

Take a screenshot. Enter the reference number if prompted.

---

## STEP 2 — READ STATUS

Take a snapshot and read the status displayed for the application.

Map portal statuses to plain language:

| Portal Text | Plain Language |
|------------|----------------|
| בטיפול / בבדיקה | Under review — background check in progress |
| ממתין לבדיקה רפואית | Awaiting medical exam — schedule and attend your medical examination |
| ממתין למסמכים | Awaiting documents — portal is waiting for additional documents |
| אושר | Approved — go to the firearms licensing office to collect your license |
| נדחה | Rejected — see reason below |
| ממתין לתשלום | Awaiting fee payment |

---

## STEP 3 — UPDATE DATA FILE AND REPORT

Update `APPLICATION.status` in `./data/<id>/applicant.md`.

Report to user:

```
══════════════════════════════════════
  Application Status
══════════════════════════════════════
Reference:   <number>
Submitted:   <date>
Status:      <plain language status>
Last checked: <now>
══════════════════════════════════════
```

Follow up based on status:

- **Approved**: Guide user to visit licensing office with ID + approval letter. Remind them to purchase weapon within 6 months and register it.
- **Awaiting medical exam**: Explain they need to visit an authorized physician (רופא מוסמך לרישוי נשק). Offer to help find one.
- **Awaiting documents**: List the documents being requested and how to submit them.
- **Rejected**: Read the rejection reason. Explain options: appeal within 30 days to the Appeals Committee (ועדת ערר) or address the stated reason.
- **Under review**: Normal — typical processing time is 30–90 days. No action needed.
