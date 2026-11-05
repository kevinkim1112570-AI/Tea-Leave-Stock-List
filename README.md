# Tea Leaves Stock List

A single-page app for listing and managing tea leaves stock: add, edit, delete, search, filter, and export to CSV.
Everything lives in `index.html`. There is no build step.

## Data storage

Data is live in Supabase (project `Inventory`, table `tea_stock`) and shared by the whole team.
Sign in with the same team accounts as the Stock In/Out List. Only signed-in users can read or change the data
(row level security). Changes made by one person appear for everyone without a refresh.

- The Supabase URL and publishable key are in `index.html`. The publishable key is meant for browsers; access is controlled by the row level security policies, not by hiding the key.
- Export CSV downloads a spreadsheet copy of the whole list.
- If someone used the older browser-only version, **Import from this browser** appears once after sign-in and moves that list into Supabase.

## Deploy to Vercel

1. In Vercel, choose **Add New > Project** and import this GitHub repository.
2. Set **Framework Preset** to **Other**. Leave Build Command and Output Directory empty.
3. Select **Deploy**.

Every push to `main` redeploys the site.

## Run locally

Open `index.html` in a browser.
