# Gymnastics Email Builder

Create SWL, Fulham and Apex Gymnastics emails using the saved club designs.

[Open the private app](https://gymnastics-email-builder.myggn2vhsf.chatgpt.site)

Choose a club, write a subject and message, optionally add a button, create a preview, then copy the complete Google Apps Script. The generated script sends highlighted spreadsheet rows sequentially and marks each result.

Download `index.html` and open it in a browser to use the app offline. No setup is required. It works entirely in your browser and saves your draft on that device. Email is sent only when you run the copied script in Google Sheets.

`source.zip` contains the maintainable module source and 33 offline tests. Generated scripts use Google's send-only mail service and access only the spreadsheet where installed.

Spreadsheet row 1: `Childs Name | Parents Name | Email | Email Status | Review` (any order). Paste the script into Extensions → Apps Script, save, reload, select rows, then use the club email menu.
