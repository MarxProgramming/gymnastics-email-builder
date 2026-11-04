# Club email builder

[Open the public app](https://marxprogramming.github.io/gymnastics-email-builder/).

A browser app for creating basic emails, term renewals and place offers for SWL Gymnastics, Fulham Gymnastics, Apex Gymnastics and Apex Dance Club. Configure the message, preview a personalised email, then copy one complete standalone Google Apps Script. SWL and Fulham retain their saved designs. Apex Gymnastics has a teal gradient header and white logo; Apex Dance uses its purple and gold website branding.

The app runs entirely in the browser. It does not connect to Gmail or send messages. Drafts are stored in local storage on the current browser. The generated script sends through the Google account running it in Google Sheets.

The password screen remembers access for 90 days in the current browser. This is a convenience gate on a public static app, not secure authentication: the password and app code remain inspectable in the published source. No password or draft content is uploaded.

## Use the app

1. Choose the club and **Basic email**, **Renewal** or **Place offer**. Each club and mode keeps its own draft on this browser.
2. For a basic email, enter a subject and body and optionally add a button with an HTTPS link. The template supplies the greeting and sign-off.
3. New renewals and offers start with the club's **Spring 2027** dates and breaks. Existing customised drafts are preserved; **Load Spring 2027 defaults** applies the preset deliberately. You can still choose **Spring**, **Summer** or **Autumn** and edit the dates. The year comes from the first term date. The calendar lets you cancel individual dates or a full week and restore them later. Choose the renewal payment deadline. Offers start with a 48-hour acceptance window, which can be changed to another window or a fixed date.
4. The club’s regular class types, days and times load automatically for both renewals and offers. SWL Gymnastics, Apex Gymnastics and Apex Dance Spring 2027 renewals also include the matching Square payment links. Review the total fee and payment link for each included class; supply links for other terms, offers and Fulham. You can deselect classes you do not need, edit a timetable when necessary, or use **Add a different class** for an extra class type. Several weekly groups can share one price/link. Combined programmes, such as SWL Senior Elite’s Wednesday and Saturday sessions, use one total fee. Add a separate class card when a weekday needs a different fee or payment link.
5. Each club’s standard membership information, payment and cancellation wording, clothing guidance, venue, Google Maps link, parent-viewing information and website links are built in. Open **Club information** to review or edit them when needed. SWL and Fulham offers include £40 annual IGA membership on top of tuition in the displayed total. Fulham membership is payable when joining and at September renewal; it has no uniform link. Apex Gymnastics offers include annual British Gymnastics sign-up information; renewals leave it out unless the annual reminder is switched on. Existing customised wording, prices, payment links and timetable edits are preserved when drafts are upgraded.
6. Choose the class to preview, then select **Create preview**. The script contains every configured class, not just the preview choice. The displayed dates and session counts reflect exclusions; fees are the total amounts you enter and are never automatically prorated.
7. Select **Copy Apps Script**, or download the `.gs` file. Any change requires a fresh preview before copying.

Use `{{child}}` and `{{parent}}` in subject or message to personalise from each row. Renewals and offers also support `{{term}}`, `{{class}}`, `{{deadline}}`, `{{fee}}` and `{{club}}`. Preview sample names are Joseph for both parent and child. Desktop and phone previews are available.

## Regular timetable defaults

Class types and weekly session times were checked against the clubs’ official websites on 3 November 2026 and are used as the ongoing defaults in both Renewal and Offer modes:

- [SWL Gymnastics](https://www.swlgymnastics.co.uk/classes): seven types, including Junior Advanced Class; Senior Elite is one combined Wednesday/Saturday programme.
- [Apex Gymnastics](https://www.apex-gymnastics.co.uk/timetable1): four types, with six Thursday groups, including two Beginners sessions and Two-Hour Advanced.
- [Apex Dance Club](https://www.apexdanceclub.co.uk/timetable1): Junior, Intermediate and Advanced Acro, with five groups across Friday and Saturday.
- [Fulham Gymnastics](https://www.fulhamgymnastics.co.uk/renewing): Beginners, Intermediate and Advanced on Mondays.

Timetables are built into the app rather than fetched when sending. Term dates, exclusions, prices, payment links and deadlines remain configurable. Every email type uses the same club header, logo, typography, button styling and footer; renewal and offer details sit inside that shared design.

## Spring 2027 defaults

The club owner supplied these term dates. Fulham's excluded Monday also matches [its venue school's half-term dates](https://www.thehurlinghamacademy.org.uk/Parents/Term-Dates).

| Club | Term window | No classes | Teaching weeks per weekly group |
|---|---|---|---:|
| SWL Gymnastics | 4 January–21 March 2027 | None | 11 |
| Fulham Gymnastics | 11 January–21 March 2027; last Monday class 15 March | 15 February | 9 |
| Apex Gymnastics | 7 January–18 March 2027 | 18 February | 10 |
| Apex Dance Club | 8 January–20 March 2027; Friday groups finish 19 March | 19 and 20 February | 10 |

Spring defaults fill new or empty advanced drafts. Existing matching Spring drafts receive missing standard fees once; other terms and customised dates are preserved. SWL, Apex Gymnastics and Apex Dance renewal drafts receive missing Square links once when their dates, regular timetable and fee match the preset. Existing edited links are preserved on automatic loading.

**Load Spring 2027 defaults** replaces dates, breaks and available standard-class fees. For SWL, Apex Gymnastics and Apex Dance renewals it also restores the matching Square payment links. Other modes and Fulham keep their existing links. Custom classes and timetable edits, notes and the chosen deadline are preserved. The total remains editable and is not recalculated when a date is later cancelled.

SWL prices use its published approximate weekly figures, as approved by the club owner. Fulham uses the same weekly rates for the matching class types at the owner's request. Apex Gymnastics rates were supplied by the owner. Apex Dance rates come from [its published timetable](https://www.apexdanceclub.co.uk/timetable1). Alternative weekly groups share the displayed price per group; SWL Senior Elite's two weekly sessions form one combined programme and are charged only once per teaching week.

| Club / class | Weekly rate | Spring renewal | Spring offer |
|---|---:|---:|---:|
| SWL Beginners | £20 | £220 | £260 |
| SWL Intermediate | £23 | £253 | £293 |
| SWL Advanced | £26 | £286 | £326 |
| SWL Junior Advanced Class | £26 | £286 | £326 |
| SWL Junior Squad | £32 | £352 | £392 |
| SWL Floor & Vault Squad | £36 | £396 | £436 |
| SWL Senior Elite, combined programme | £73 | £803 | £843 |
| Fulham Beginners | £20 | £180 | £220 |
| Fulham Intermediate | £23 | £207 | £247 |
| Fulham Advanced | £26 | £234 | £274 |
| Apex Gymnastics Beginners | £15 | £150 | £150 |
| Apex Gymnastics Intermediate | £17 | £170 | £170 |
| Apex Gymnastics Advanced | £20 | £200 | £200 |
| Apex Gymnastics Two-Hour Advanced | £34 | £340 | £340 |
| Apex Dance Junior Acro | £14 | £140 | £140 |
| Apex Dance Intermediate Acro | £16 | £160 | £160 |
| Apex Dance Advanced Acro | £16 | £160 | £160 |

SWL/Fulham Offer totals include £40 membership once. These Spring renewal totals add no membership charge. Apex Gymnastics British Gymnastics membership remains separate.

The 14 Square links built into the three clubs' Spring renewal presets were checked on 4 November 2026 against the class titles and prices above. Each asks for one required **Child's name** field. The payment buttons in previews and generated Apps Scripts use these same links. A known Square link must match its fixed checkout price before a preview or script can be generated; a different fee needs a corresponding payment link. Renewal links are not inserted into offers or Fulham.

## Standard club information

Club details were checked on 4 November 2026 against the supplied email examples and the clubs’ public information pages: [SWL rules](https://www.swlgymnastics.co.uk/club-rules), [Fulham FAQ](https://www.fulhamgymnastics.co.uk/faq), [Fulham renewal information](https://www.fulhamgymnastics.co.uk/renewing), [Apex Gymnastics rules](https://www.apex-gymnastics.co.uk/club-rules) and [Apex Dance policies](https://www.apexdanceclub.co.uk/club-rules). Each mode has its own payment and cancellation wording. The latest club instructions apply to every offer: the first term is commitment-free, with a refund for remaining classes not yet attended if a child decides not to continue for any reason. All clubs say parent viewing is usually the second-to-last class of term, with details sent nearer the date. SWL’s location uses its current public West Hill address, matching the existing email footer.

Apex Dance includes an optional dancewear suggestion from the supplied clothing email; it does not require buying a uniform. Fulham has no uniform button. Fulham recommends comfortable sportswear or a leotard, without a statement about buying uniform. Standard information remains editable and is copied into the generated script, not fetched when sending.

Draft upgrades refresh unchanged standard wording while keeping custom edits and deliberate removals. The email details panel uses a uniform outline and lists only the class, term dates, total teaching weeks, total fee, deadline and class-specific cancellations; renewal deadlines are highlighted in red. The optional annual British Gymnastics reminder is specific to Apex Gymnastics Renewal; it changes only standard reminder wording, preserving separately customised membership text and links.

## Use the script in Google Sheets

Include headings for the child, parent and recipient email in one row within the first 20 rows, in any column order:

`Childs Name | Parents Name | Email`

Common variations are accepted, including `Child Name`, `Child’s First Name`, `Parent Name`, `Parent One`, `Parent 1`, `Guardian Name`, `Email Address` and `Parent Email`. The sender normalises apostrophes, punctuation, letter case and spacing. Names and a valid email are required for each recipient. Multiple possible heading rows or two recognised columns for the same role produce an actionable error instead of guessing. `PARENT2`, phone columns and attendance dates are not mistaken for the required fields.

`Email Status` is added automatically at the first column after all existing data when the first eligible email is sent. Existing attendance, notes and contact columns are preserved. A `Review` column is optional; if present, its existing skip behaviour is retained. Checking rows never adds columns or changes cells.

Open **Extensions → Apps Script** from the spreadsheet, replace the starter code with the complete generated script, save, then reopen or reload the spreadsheet. Every generated script starts with `onOpen()`, which adds the club email menu automatically. No setup function, manual trigger or class selection is needed to open the sheet. Opening only adds the menu; it never sends emails. Preserve existing scripts if you add this to an established project: replace the previous builder script rather than appending another full script, because their shared function names would collide. If the project already has an unrelated `onOpen`, merge its menu code into the one opening function.

Highlight your intended rows, then use the club email menu:

- **Check selected rows (no email)** for basic emails, or **Choose class & check rows (no email)** for renewals and offers, opens a result dialog showing the heading row, mapped columns, eligible count, skip reasons and any planned Email Status column. It sends nothing and changes no cells.
- **Send selected emails** starts immediately for basic emails.
- **Choose class & send selected rows** in renewal and offer scripts asks you to choose a numbered class, then sends that class’s email to the highlighted rows, one row at a time. The builder’s preview choice does not preselect the class in Sheets. Cancelling the class choice sends nothing. Each result is recorded in Email Status. Every eligible selected row is sent again on a new manual invocation, regardless of any previous Email Status—including sent, interrupted or error statuses.

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
