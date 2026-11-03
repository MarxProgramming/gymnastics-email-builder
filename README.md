# Club email builder

[Open the public app](https://marxprogramming.github.io/gymnastics-email-builder/).

A browser app for creating basic emails, term renewals and place offers for SWL Gymnastics, Fulham Gymnastics, Apex Gymnastics and Apex Dance Club. Configure the message, preview a personalised email, then copy one complete standalone Google Apps Script. SWL and Fulham retain their saved designs. Apex Gymnastics has a teal gradient header and white logo; Apex Dance uses its purple and gold website branding.

The app runs entirely in the browser. It does not connect to Gmail or send messages. Drafts are stored in local storage on the current browser. The generated script sends through the Google account running it in Google Sheets.

The password screen remembers access for 90 days in the current browser. This is a convenience gate on a public static app, not secure authentication: the password and app code remain inspectable in the published source. No password or draft content is uploaded.

## Use the app

1. Choose the club and **Basic email**, **Renewal** or **Place offer**. Each club and mode keeps its own draft on this browser.
2. For a basic email, enter a subject and body and optionally add a button with an HTTPS link. The template supplies the greeting and sign-off.
3. For renewals and offers, set the term name and start/end dates. The calendar lets you cancel individual dates or a full week and restore them later. Enter the payment deadline; offers can instead use an acceptance window in hours.
4. Add the class types you need, with the total term fee, payment link, and weekly days/times. Several session choices can share one price/link. Mark a class as a combined programme only when the same child attends all of its sessions. Add a separate class card when a weekday needs a different fee or payment link.
5. Add any extra information, membership note, payment instructions or offer details. Dates, fees, links and policies from old example campaigns are not automatically treated as current. SWL and Apex timetable suggestions remain editable; Fulham and Apex Dance accept your own classes.
6. Choose the class to preview, then select **Create preview**. The script contains every configured class, not just the preview choice. The displayed dates and session counts reflect exclusions; fees are the total amounts you enter and are never automatically prorated.
7. Select **Copy Apps Script**, or download the `.gs` file. Any change requires a fresh preview before copying.

Use `{{child}}` and `{{parent}}` in subject or message to personalise from each row. Renewals and offers also support `{{term}}`, `{{class}}`, `{{deadline}}`, `{{fee}}` and `{{club}}`. Preview sample names are Joseph for both parent and child. Desktop and phone previews are available.

## Use the script in Google Sheets

Include headings for the child, parent and recipient email in one row within the first 20 rows, in any column order:

`Childs Name | Parents Name | Email`

Common variations are accepted, including `Child Name`, `Child’s First Name`, `Parent Name`, `Parent One`, `Parent 1`, `Guardian Name`, `Email Address` and `Parent Email`. The sender normalises apostrophes, punctuation, letter case and spacing. Names and a valid email are required for each recipient. Multiple possible heading rows or two recognised columns for the same role produce an actionable error instead of guessing. `PARENT2`, phone columns and attendance dates are not mistaken for the required fields.

`Email Status` is added automatically at the first column after all existing data when the first eligible email is sent. Existing attendance, notes and contact columns are preserved. A `Review` column is optional; if present, its existing skip behaviour is retained. Checking rows never adds columns or changes cells.

Open **Extensions → Apps Script** in a new spreadsheet, replace the starter code with the complete generated script, save, then reload the sheet. Preserve existing scripts if you add this to an established project: do not paste multiple full club scripts into one project because their shared function names would collide.

Highlight your intended rows, then use the club email menu:

- **Check selected rows (no email)** opens a result dialog showing the heading row, mapped columns, eligible count, skip reasons and any planned Email Status column. It sends nothing and changes no cells.
- **Send selected emails** starts immediately for basic emails. Renewal and offer scripts first ask you to choose a numbered class, then send that class’s email to the highlighted rows, one row at a time. Cancelling the class choice sends nothing. Each result is recorded in Email Status. Every eligible selected row is sent again on a new manual invocation, regardless of any previous Email Status—including sent, interrupted or error statuses.

The script deduplicates overlapping row selections within each send. It skips rows with nonblank Review, missing names or invalid email addresses, and rows hidden manually or by a standard filter. Google filter views are not detected. Siblings sharing an email address receive separate emails. Sending stops before the time limit or when the available email quota is exhausted; select only the remaining unsent rows to continue, because selecting previously sent rows sends another email. A document lock prevents overlapping send runs. The script does not automatically retry failed rows. If a send was interrupted, check Sent mail before selecting that row again.

Use the appropriate club Google account. Google may require first-use authorisation. There is no need to clear Email Status for a new message or to resend: it records the latest result and is never used as an eligibility filter.

## Development

No dependencies or build are needed. The `dist` folder is the complete static website. Serve it over HTTP (ES modules cannot reliably load from `file://`):

```sh
npm run preview
npm run check
npm test
```

Open `http://localhost:4173` after starting the preview server. Publish the contents of `dist` using static hosting, or a GitHub Pages workflow that uploads `dist`.

The engine replaces the email-content function and uses the send-only MailApp service. Advanced modes add calendar-derived class details, styled sections and payment links within the club design. The Apps Script class prompt runs before the document lock; selected rows and their sheet are captured before the prompt opens. All four app-owned templates share a sender that detects headings and adds tracking safely. SWL and Fulham email designs remain unchanged; the Apex Gymnastics and Apex Dance variants retain their requested branding. Original templates on the desktop are never edited. Generated script inputs are encoded as data, and personalisation is escaped in the rendered email.

Run `node scripts/build-senders.mjs` after changing `scripts/selected-row-sender.gs` to apply the shared sender to all four app templates. Run `node scripts/build-templates.mjs` after changing an email design to regenerate the exact preview functions. Run `node scripts/build-standalone.mjs` to create a single offline file at `build/index.html`, or pass an explicit destination path. This file embeds the app, gate, templates and images without external dependencies. The optional `build-variants.mjs` helper recreates the two app-owned variants from an original Apex template folder and the supplied brand PNGs, then applies the current shared sender.

Offline tests use mocked Google services and must not be described as real delivery tests. A live delivery test requires an explicitly authorised recipient and a signed-in Google account.
