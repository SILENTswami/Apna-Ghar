# Apna Ghar Vanshavali

A family tree website with no server. The whole tree lives in `family.json` in this repository, and every device reads that one shared copy.

Live site: https://silentswami.github.io/Apna-Ghar/

## Files

- `index.html` — the site. It also carries a backup copy of the starting data, used only if GitHub can't be reached.
- `family.json` — the family: names, nicknames, gotra, notes, photos, the chosen style, the admin password hash and the locked GitHub token.

## First-time setup

1. Open the site and click **Admin**. Choose a password (at least 8 characters; longer is safer).
2. Connect GitHub once, so your edits save for everyone:
   1. On GitHub go to **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
   2. Under **Repository access** pick **Only select repositories → Apna-Ghar**.
   3. Under **Permissions → Repository permissions** set **Contents** to **Read and write**.
   4. Copy the token. In the tree, open **Family file**, paste it, enter your admin password and click **Connect GitHub**.
3. Tap your own portrait ("Your name"), then **Edit details** to enter your name.
4. Grow the tree in any direction: **+ Parents** above the eldest person, **+ Spouse**, **+ Child**, and **Add brother or sister** in the details panel.
   Generation numbers (पीढ़ी १, २, ३…) are worked out from the eldest person, so they renumber automatically whenever you add parents above.
   For someone who married into the family, the edit form also takes their father's and mother's names.

## How syncing works

- **Every visitor** loads the latest `family.json` straight from GitHub.
- **Each admin edit** is committed to `family.json` within a couple of seconds. The header shows the state: *Saving for everyone…*, *Saved for everyone*, or *Saved on this device only* when GitHub isn't connected.
- **After each save** the page sends an update signal through [ntfy.sh](https://ntfy.sh) (a free notification relay). Every open copy of the tree listens for it and reloads `family.json` from GitHub, so changes appear on other devices within seconds. A tree also checks once when you come back to its tab, because phones pause connections while the screen is off.
- The signal only says "something changed"; the data itself always comes from GitHub, so a fake signal can do no harm beyond a reload.
- **Other devices:** unlock Admin with the same password. The GitHub token is stored in `family.json` encrypted with that password, so you don't need to enter it again.
- **Two edits at once:** if the tree changed on another device before your save landed, your device loads the newer version and asks you to redo your last change.
- **History:** every save is a commit, so any earlier version can be restored from the repository's history.

## Security notes

- The admin password is stored only as a salted PBKDF2 hash. It hides the editing tools; the real protection is that writing to GitHub needs the token.
- The token is encrypted (AES-GCM, key derived from the admin password with PBKDF2). Because the repository is public, use a strong password, and give the token access to this one repository only.
- If the token ever leaks, delete it on GitHub, create a new one and connect again.

## Backups

**Family file → Download family.json** or **Copy as text** keeps a copy. **Open file** / **Load pasted text** loads one back in, replacing the tree for everyone.

## Photos

Uploaded photos are cropped and shrunk to about 25 KB each and stored inside `family.json`. A tree of a few hundred people with photos stays a few MB.
