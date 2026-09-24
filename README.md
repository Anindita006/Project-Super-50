# Super50 Dashboard — GitHub Pages + Supabase

This package makes the Super50 dashboard shared across all viewers.

## How it works

Administrator Excel upload
-> Supabase database
-> Supabase Realtime
-> every open dashboard updates automatically

GitHub Pages hosts only the dashboard files. The Excel data is stored in Supabase.

## 1. Create a Supabase project

Create a project at https://supabase.com/

Then go to:
Authentication -> Users -> Add user

Create the administrator email/password.

## 2. Run the SQL

Open:
SQL Editor -> New query

Open `Supabase_Setup.sql`, replace:

YOUR_ADMIN_EMAIL@example.com

with the administrator email, then run the SQL.

If Supabase reports that `dashboard_data` is already in `supabase_realtime`, that is harmless.

## 3. Configure the dashboard

Open `config.js` and replace:

- SUPER50_SUPABASE_URL
- SUPER50_SUPABASE_ANON_KEY
- SUPER50_ADMIN_EMAILS

Use the Supabase Project URL and the browser-safe publishable/anon key.

NEVER put the service-role/secret key in this file.

## 4. Publish on GitHub Pages

Upload these two files to the root of your GitHub repository:

- index.html
- config.js

Then:
GitHub repository -> Settings -> Pages -> Deploy from branch -> main -> root.

Your dashboard will get a GitHub Pages URL.

## 5. Data behavior

Anyone with the URL can view the dashboard.

Only the Supabase administrator account can upload/update:

- DT data
- Village loss data
- Feeder loss trend
- Action taken

After an upload, Supabase Realtime sends the new data to open dashboards.

A person opening the URL later receives the latest saved data.

## Important security note

The publishable/anon key is designed to be used in browser code when Row Level Security is enabled.

Never publish the Supabase service-role/secret key.

The administrator password is handled by Supabase Authentication and is not stored in the HTML.

## Excel upload

Continue using the same Excel formats expected by the dashboard.

For Action Taken, the current format supports:

Circle | Model_Village | Action_Taken | Action_Count

`Action_Count` can be used for aggregate action totals. If individual Model_Village names are supplied, clicking action counts can show the village names.

## Updating dashboard code

You do NOT upload the Excel file to GitHub.

GitHub is only for the dashboard code.

Upload Excel through the administrator controls in the dashboard.

