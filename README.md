# Paperly — GitHub + Supabase

This version of Paperly uses:
- GitHub Pages for hosting the web app.
- IndexedDB for local/offline notebook storage.
- Supabase Auth + Postgres for cross-device notebook sync.

## Setup

1. Create a free Supabase project.
2. Open **SQL Editor** and run `supabase.sql`.
3. In Supabase, open the project's **Connect** dialog / API settings and copy the Project URL and **publishable** key. Do not use a secret/service_role key in the browser.
4. Put those two values in `paperly-config.js`.
5. Create a GitHub repository and upload `index.html` and `paperly-config.js`. Keep `supabase.sql` in the repo if you want, but it is not loaded by the app.
6. Enable GitHub Pages for the repository.
7. Open the published Paperly URL on your laptop, click **Sync**, create an account, and then use the same account on your Samsung tablet.

## Notes

The current cloud sync stores each notebook as JSONB. That keeps the setup simple and free for personal use, but very large collections of embedded PDF/image base64 data can consume the Supabase database quota. The next performance upgrade should move binary assets into Supabase Storage and keep only asset IDs/metadata in notebook JSON.

Supabase's current free plan includes 500 MB database size and 1 GB file storage; projects can pause after 1 week of inactivity. Check Supabase's current pricing before relying on it for large-scale storage.
