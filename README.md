# Tea Leaves Stock List

A single-page app for listing and managing tea leaves stock: add, edit, delete, search, filter, and export to CSV.
Everything lives in `index.html`. There is no build step and no dependencies.

## Data storage

Data is saved in the browser's local storage, so each browser keeps its own list.
Use **Backup** (JSON) or **Export CSV** regularly, and **Restore** to load a backup.

## Deploy to Vercel

1. In Vercel, choose **Add New > Project** and import this GitHub repository.
2. Set **Framework Preset** to **Other**. Leave Build Command and Output Directory empty.
3. Select **Deploy**.

Every push to `main` redeploys the site.

## Run locally

Open `index.html` in a browser.
