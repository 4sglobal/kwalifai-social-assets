# Publishing this folder as a public GitHub repo

This folder is the staging area for `kwalifai-social-assets`, the public CDN
repository Buffer will fetch images from. The folder contains:

- 102 PNG images (Pilot-Set-v3 library + launch graphics)
- README.md, LICENSE.txt, .gitignore
- A half-initialized `.git/` directory that needs to be removed (the Claude
  sandbox could not finish the init due to filesystem permissions). Your
  Windows terminal will clean it up in one command below.

## One-time setup (about 5 minutes)

### Step 1. Create the empty repo on GitHub.com

1. Go to https://github.com/new
2. Owner: `4sglobal`
3. Repository name: `kwalifai-social-assets` (exact, lowercase, with hyphens)
4. Description: `Public CDN for Kwalifai (NMLS 2528067, 4S Global, LLC) social media images`
5. **Public** (this is intentional - marketing images are inherently public)
6. Do NOT initialize with a README, .gitignore, or license (we already have them)
7. Click Create repository

### Step 2. Open PowerShell and publish

Paste these commands as a block:

```powershell
cd C:\Users\sriga\Kwalifaiv2\Kwalifai-You-Mortgage-Rate-Finder-\Kwalifai-Launch-Kit\_social-assets-repo-ready

# Remove the half-init .git directory the Claude sandbox created
Remove-Item -Recurse -Force .git

# Fresh git init + commit + push
git init -b main
git config user.email "admin@kwalifai.com"
git config user.name "Kwalifai Brand"
git add .
git commit -m "feat: initial commit of Kwalifai social assets for Buffer CDN"
git remote add origin https://github.com/4sglobal/kwalifai-social-assets.git
git push -u origin main
```

GitHub will prompt for credentials on `git push`. Use your standard GitHub
authentication (Personal Access Token in your credential manager, or
GitHub CLI).

### Step 3. Wait 60 seconds, then verify one URL

After the push succeeds, wait about a minute for the GitHub CDN to warm up,
then open this URL in a browser:

https://raw.githubusercontent.com/4sglobal/kwalifai-social-assets/main/Pilot-Set-v3/01-wall-street-frontrun.png

You should see the Wall Street front-running image render. If you do, the CDN
is live and Buffer can fetch every other URL the same way.

### Step 4. Upload the Buffer CSVs

Open Buffer (https://buffer.com). For each channel, go to the channel queue,
click the three-dot menu, then Bulk Upload. Upload these files from
`Kwalifai-Launch-Kit/buffer-bulk-upload/`:

- `buffer-bulk-instagram.csv` (84 posts)
- `buffer-bulk-facebook.csv` (84 posts)
- `buffer-bulk-linkedin.csv` (60 posts, 36 with images + 24 text-only)
- `buffer-bulk-youtube.csv` (60 posts)

Buffer reads the Image URL column directly from these CSVs, fetches each
image from your public repo, and queues the post with the image already
attached. No manual attachment step.

### One thing to do first in Buffer: create the tags

The Tags column in each CSV uses these labels:

`single`, `carousel`, `story`, `reel`, `short`, `founder-pov`, `long-form`,
`yt-community`, `recap`, `quote`

In Buffer, go to Library -> Tags -> Create new tag. Make all ten of those.
Then the bulk upload will associate each post with the right tag, which
makes filtering the queue trivial later.

## What about updates later?

When you add or change an image, you:

1. Drop the new PNG into the right subfolder inside this `_social-assets-repo-ready/`
2. Run from this folder: `git add . && git commit -m "..." && git push`
3. The new URL is live within 60 seconds at the same `raw.githubusercontent.com` path

Ask Claude to re-run the calendar generator any time the captions change in the
source markdown files - Claude will rebuild the four CSVs in under a minute.

## License and brand reminder

All images here are owned by 4S Global, LLC and used exclusively under the
Kwalifai brand (NMLS 2528067). LICENSE.txt has the legal text. They are made
public for the operational purpose of feeding social schedulers, not for
third-party reuse.
