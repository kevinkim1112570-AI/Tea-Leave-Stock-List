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

## Dashboard

The **Dashboard** button opens two lists that the Add Stock form uses:

- **Category List**: one column per Category, listing its Sub. Category choices. Edit a name in place, type in the empty cell at the bottom of a column to add one, or use the x to remove one.
- **Place No. and Place Code**: Place No. 1 to 90 is fixed, only the Place Code can be changed. In Add Stock you pick or type the Place Code and the Place No. fills in by itself: an existing code gives its Place No., and a new code takes the lowest Place No. that has no code yet and is added to this list. Each Place Code belongs to one Place No.

Both lists live in Supabase (`tea_sub_categories`, `tea_places`) and update live for everyone.

## Accounts and approval

The login page has a **Create Account** button. Anyone can register, but a new account only sees a "Waiting for approval" screen until it is added to the `tea_members` table in Supabase (Table Editor → `tea_members` → Insert row → paste the user's id from Authentication → Users). The tea tables (`tea_stock`, `tea_places`, `tea_sub_categories`) are readable and editable by approved members only. Accounts that existed before this feature were approved automatically.

**Admin page:** the Admin button on the login page asks for the Admin password, then lists every account. Tick **Read Only** (can view, cannot change anything) or **Edit Access** (can change the list); tick neither to keep the account waiting. Edit sets a new password, Delete removes the account. Passwords cannot be shown because Supabase only keeps them scrambled. The Admin password is checked by the `tea-admin` Edge Function using the secret `TEA_ADMIN_PASSWORD` (Supabase → Edge Functions → Secrets), not in the web page. Five wrong tries lock it for 15 minutes.

In the Supabase dashboard (Authentication) also check: sign-ups are enabled, and **Site URL** is your Vercel address so confirmation emails link back to the app.

## Deploy to Vercel

1. In Vercel, choose **Add New > Project** and import this GitHub repository.
2. Set **Framework Preset** to **Other**. Leave Build Command and Output Directory empty.
3. Select **Deploy**.

Every push to `main` redeploys the site.

## Run locally

Open `index.html` in a browser.
