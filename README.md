# CopyrightKiller releases site (public repo template)

Copy the contents of this folder into a **public** GitHub repo named `CopyrightKiller-releases`.

## One-time setup

1. Create a new **public** repo: `CopyrightKiller-releases` (under the same GitHub account as the main app).
2. Copy these files to the repo root:
   - `docs/index.html` → `docs/index.html`
   - `updates/latest.json` → `updates/latest.json`
3. Enable **GitHub Pages**: repo **Settings → Pages →** source **main** branch, folder **/docs**.
4. Your download page will be at:
   `https://samstriker2938429310478097.github.io/CopyrightKiller-releases/`
5. On the **private** copyrightkiller repo, add secrets:
   - **`RELEASES_REPO_TOKEN`** — fine-grained PAT with **write** access to `CopyrightKiller-releases` only
   - **`GOOGLE_OAUTH_CREDENTIALS_JSON`** — full contents of your Google `credentials.json` (baked into Mac/Windows builds; never commit that file)

## Team password

The download page is gated with a team password. **Do not commit the plaintext password** — only the SHA-256 hash belongs in `docs/index.html`.

Share the password with teammates out of band (chat, 1Password, etc.).

To rotate the password:

1. Open `tools/hash-password.html` in your browser (locally).
2. Enter the new password and copy the SHA-256 hash.
3. Paste the hash into `docs/index.html` as `PASSWORD_HASH`.
4. Commit and push to the public releases repo.
5. Tell the team the new password privately.

This is casual protection (not bank-grade). Anyone technical can still find GitHub release asset URLs.

## What CI updates automatically

When you push a version tag (`v0.1.0`) on the private copyrightkiller repo, GitHub Actions will:

- Build Mac Apple Silicon + Intel (`.app` → two `.dmg` files) and Windows (exe + ffmpeg zip) with Google credentials baked in
- Create a GitHub Release on `CopyrightKiller-releases`
- Update `updates/latest.json` with direct download URLs (`mac_arm64_url`, `mac_intel_url`, `windows_url`)

You do **not** need to edit `latest.json` by hand after the first setup.
