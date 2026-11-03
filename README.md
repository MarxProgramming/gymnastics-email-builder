# Club email builder

[Open the public app](https://marxprogramming.github.io/gymnastics-email-builder/).

A simple browser app for creating branded emails for SWL Gymnastics, Fulham Gymnastics, Apex Gymnastics and Apex Dance Club. Choose a club, enter a subject and message, optionally add one button, then create a preview and copy the complete standalone Google Apps Script. SWL and Fulham retain their saved designs. Apex Gymnastics has a teal gradient header and white logo; Apex Dance uses its purple and gold website branding.

The app runs entirely in the browser. It does not connect to Gmail or send messages. Drafts are stored in local storage on the current browser. The generated script sends through the Google account running it in Google Sheets.

The password screen remembers access for 90 days in the current browser. This is a convenience gate on a public static app, not secure authentication: the password and app code remain inspectable in the published source. No password or draft content is uploaded.

## Use the app

1. Choose the club and enter your subject and body. The template adds the greeting and sign-off.
2. Use `{{child}}` and `{{parent}}` in your subject or body to insert names from each spreadsheet row. The name buttons insert at your last position in the subject or body.
3. Optionally add a button with a label and a complete HTTPS link.
4. Select **Create preview**. The preview uses Joseph for both sample names and your selected club branding. Desktop and phone preview widths are available.
5. Select **Copy Apps Script**, or download the `.gs` file. If you edit your message or change club after previewing, create a new preview before copying.

## Use the script in Google Sheets

Include headings for the child, parent and recipient email in one row within the first 20 rows, in any column order:

`Childs Name | Parents Name | Email`

Common variations are accepted, including `Child Name`, `Child’s First Name`, `Parent Name`, `Guardian Name`, `Email Address` and `Parent Email`. The sender normalises apostrophes, punctuation, letter case and spacing. Names and a valid email are required for each recipient. Multiple possible heading rows or two recognised columns for the same role produce an actionable error instead of guessing. `PARENT2`, phone columns and attendance dates are not mistaken for the required fields.

`Email Status` is added automatically at the first column after all existing data when the first eligible email is sent. Existing attendance, notes and contact columns are preserved. A `Review` column is optional; if present, its existing skip behaviour is retained. Checking rows never adds columns or changes cells.

Open **Extensions → Apps Script** in a new spreadsheet, replace the starter code with the complete generated script, save, then reload the sheet. Preserve existing scripts if you add this to an established project: do not paste multiple full club scripts into one project because their shared function names would collide.

Highlight your intended rows, then use the club email menu:

- **Check selected rows (no email)** opens a result dialog showing the heading row, mapped columns, eligible count, skip reasons and any planned Email Status column. It sends nothing and changes no cells.
- **Send selected emails** starts immediately, one row at a time, and records each result in Email Status.

The script deduplicates overlapping row selections, skips rows with nonblank Email Status or Review, and skips rows hidden manually or by a standard filter. Google filter views are not detected. Siblings sharing an email address receive separate emails. Sending stops before the time limit or when the available email quota is exhausted; reselect the same rows later to continue. A document lock prevents overlapping send runs. Ambiguous or interrupted sends retain a status so they are not automatically sent again: check Sent mail before clearing a status.

Use the appropriate club Google account. Google may require first-use authorisation. A new campaign needs a fresh copy with blank statuses, or deliberately cleared statuses for only the rows to send again.

## Development

No dependencies or build are needed. The `dist` folder is the complete static website. Serve it over HTTP (ES modules cannot reliably load from `file://`):

```sh
npm run preview
npm run check
npm test
```

Open `http://localhost:4173` after starting the preview server. Publish the contents of `dist` using static hosting, or a GitHub Pages workflow that uploads `dist`.

The engine replaces the email-content function and uses the send-only MailApp service. All four app-owned templates share a sender that detects headings and adds tracking safely. SWL and Fulham email designs remain unchanged; the Apex Gymnastics and Apex Dance variants retain their requested branding. Original templates on the desktop are never edited. Generated script inputs are encoded as data, and personalisation is escaped in the rendered email.

Run `node scripts/build-senders.mjs` after changing `scripts/selected-row-sender.gs` to apply the shared sender to all four app templates. Run `node scripts/build-templates.mjs` after changing an email design to regenerate the exact preview functions. Run `node scripts/build-standalone.mjs` to create a single offline file at `build/index.html`, or pass an explicit destination path. This file embeds the app, gate, templates and images without external dependencies. The optional `build-variants.mjs` helper recreates the two app-owned variants from an original Apex template folder and the supplied brand PNGs, then applies the current shared sender.

Offline tests use mocked Google services and must not be described as real delivery tests. A live delivery test requires an explicitly authorised recipient and a signed-in Google account.
