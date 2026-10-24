# Apna Ghar Vanshavali

A static family tree site. No server or database: the whole tree lives in `family.json`.

## Files

- `index.html` — the site. It also carries a backup copy of the starting family data, used only when `family.json` can't be read.
- `family.json` — your family: names, nicknames, gotra, notes, photos, the chosen style and the admin password hash.

## First-time setup

1. Open the site and click **Admin**. Choose a password (at least 6 characters).
2. Pick a look under **Style** (colour, portrait frame, branch lines).
3. Tap your own portrait ("Your name"), then **Edit details** to enter your name.
4. Grow the tree in any direction: **+ Parents** above the eldest person, **+ Spouse**, **+ Child**, and **Add brother or sister** in the details panel.
   Generation numbers (पीढ़ी १, २, ३…) are worked out from the eldest person, so they renumber automatically whenever you add parents above.
   For someone who married into the family, the edit form also takes their father's and mother's names.

## Publishing your edits

Edits save in your own browser first. To show them to everyone:

1. Click **Family file → Download family.json**.
2. Replace `family.json` where the site is hosted.

Until you do this, only your browser sees the changes.

## Hosting

Any static host works: GitHub Pages, Netlify, Cloudflare Pages, or a plain web server. Upload `index.html` and `family.json` together.
Opening `index.html` straight from your computer shows the built-in backup data, not `family.json`, because browsers block reading local files.

## About the password

The password is stored only as a salted hash inside `family.json`, and it hides the editing tools from family members.
It is not server-side security. Because there is no server, nobody can change the published tree without replacing `family.json` on the host, and that is what really protects it.

## Photos

Uploaded photos are cropped and shrunk to about 25 KB each and stored inside `family.json`. A tree of a few hundred people with photos stays a few MB.
