# get.bearlyinvested.app: smart store links

Social bio links that send phones straight to the right store, with a branded fallback page
for desktop users or when a redirect is blocked.

| URL | iPhone / iPad | Android |
| --- | --- | --- |
| `/ig` | App Store, campaign `ct=ig-bio` | Google Play |
| `/yt` | App Store, campaign `ct=yt-bio` | Google Play |
| `/tt` | App Store (untracked for now) | Google Play |
| `/` or anything else (404) | App Store (untracked) | Google Play |

`index.html`, `ig.html`, `tt.html`, `yt.html` and `404.html` are **identical**. The page reads its
own path to pick the campaign. Edit `index.html`, then re-copy:

```bash
for f in ig tt yt 404; do cp index.html $f.html; done
```

To add a channel, add it to `CAMPAIGNS` in the head script and create `<slug>.html` as a copy.
Apple campaign tokens (`ct`) are free-form, so a new one needs no setup in App Store Connect.

Add `?stay` to any URL to view the page on a phone without being redirected.

## Hosting (GitHub Pages)

GitHub Pages allows **one custom domain per repo**, and `bearlyinvested.app` already uses the
`bearlyinvested-site` repo. So this folder needs its own repo:

1. Push the contents of `get-site/` to a new repo (e.g. `NinadBhide/bearlyinvested-get`).
2. Repo → Settings → Pages → deploy from `main` / root. Custom domain: `get.bearlyinvested.app`
   (the `CNAME` file already declares it).
3. Name.com DNS: add `CNAME  get  ninadbhide.github.io`.
4. Wait for the certificate, then tick **Enforce HTTPS**. `.app` is HTTPS-only, so the links
   will not load at all until the certificate is issued.

Local preview: `npx serve -l 4174 .` from this folder (also the `get-site` entry in `.claude/launch.json`).
