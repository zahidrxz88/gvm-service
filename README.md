# GVM AV Systems (combined)

A single entry point that switches between two independent dashboards using a
top-right toggle. No data is shared or merged between them — each is a
separate self-contained app talking to its own separate Supabase project.

- `index.html` — the shell/switcher. Deploy this whole folder as-is.
- `gvm-tracker.html` — GVM PM Tracker (default dashboard on load).
- `adhoc-token.html` — Adhoc / Token System.

## Deploy

Any static host works (Netlify, Vercel, GitHub Pages, etc.) — just publish
this folder. `index.html` must stay in the same folder as the other two
files since it references them by relative filename.

## Notes

- Always opens on the PM Tracker; the last-viewed dashboard is not remembered.
- Editing either dashboard's own logic/styling: edit `gvm-tracker.html` or
  `adhoc-token.html` directly — they're unmodified copies of the originals.
- Editing the toggle/shell: edit `index.html`.
