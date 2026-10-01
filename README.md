# Orbit

A shared board for the team's AI and automation ideas: who pitched each one, who's building it, what it costs, how risky it is, and where it stands.

**Live board:** https://attano26.github.io/Orbit/

## How it works

- **The website is one file.** `index.html` holds the whole board and needs no build step or server. GitHub Pages serves it as it is.
- **The data lives in Supabase, not in this repo.** Ideas, people, labels, AI tools, technologies and repositories are all stored in one Supabase table, `items`.
- **Only invited people can get in.** Visitors see a sign-in screen. Row-level security in the database lets signed-in team members read and change items. Anyone else gets nothing back.
- **Changes appear live.** When one person edits an idea, everyone else's board updates without a refresh.

The Supabase key in `index.html` is the public "anon" key. It's meant to sit in browser code, and the row-level security rules are what protect the data. Never put a `service_role` or `sb_secret_` key in this file.

## Files

| File | What it is |
|---|---|
| `index.html` | The board. |
| `.nojekyll` | An empty file that tells GitHub Pages to serve `index.html` as it is, without running Jekyll first. |
| `README.md` | This page. |

The one-time database script (`setup.sql`) is **not** in this repo, because it contains the team's ideas and names. It stays in the private project folder.

## First-time setup (already done)

1. **Database.** In Supabase, open SQL Editor → New query, paste `setup.sql`, and click Run. This creates the `items` table and its access rules, turns on live updates, and loads the starting ideas.
2. **Website.** Go to Settings → Pages → Branch, choose `main` and `/ (root)`, and click Save.
3. **Password-reset links.** In Supabase, go to Authentication → URL Configuration and set Site URL to `https://attano26.github.io/Orbit/`. Without this, reset emails point to the wrong address.

## Managing people

In Supabase, go to **Authentication → Users**.

- **Add someone.** Click Add user, enter their email and a password, and tick Auto Confirm User.
- **Remove someone.** Delete the user. They can't sign in again.
- **Forgotten password.** The person clicks Forgot password? on the sign-in screen and gets an email with a reset link.

## Updating the board

Replace `index.html` in this repo with the new version: Add file → Upload files, then Commit changes. The live board updates within a minute or two. To see it immediately, hard-refresh with Ctrl+Shift+R.

Ideas aren't affected, because they live in Supabase and not in the file.

## Backups

In Supabase, go to **Table Editor → items → Export to CSV**. Do this before any big change.
