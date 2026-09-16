# Funders Founders World

The website for [fundersfounders.world](https://www.fundersfounders.world/), rebuilt as a plain static site so it can be hosted for free on GitHub Pages.

- No framework, no build step. Edit the HTML and push.
- One stylesheet (`assets/css/site.css`), one small script (`assets/js/site.js`).
- Every image lives in `assets/img/`, so nothing depends on Google's servers.

## Pages

| Path | File |
|---|---|
| `/` | `index.html` |
| `/mxr-ai/` | `mxr-ai/index.html` |
| `/privacy-policy/` | `privacy-policy/index.html` |
| `/terms-of-service/` | `terms-of-service/index.html` |
| `/home` | `home/index.html` (redirects to `/`, keeps the old Google Sites URL working) |
| any missing page | `404.html` |

## Editing content

Open the HTML file for the page and change the text. The homepage sections, in order: hero, the upcoming Lake Como delegation, "What's in it for you", the three programme formats, "Who is this for", the previous-editions board, the network logos, the FAQ, and the closing call to action.

To add a past event, copy one `board-row` block in `index.html`, change the airport code, city, title, description, image and link. To add an FAQ, copy one `details` block.

The "Talk to MXR Agent" chat widget is the Voiceflow snippet at the bottom of every page. Its project ID is the only thing you would ever change there.

## Preview locally

Any static server works. For example:

```bash
python3 -m http.server 8479
```

Then open http://localhost:8479/.

## Publish on GitHub Pages

1. Create a GitHub repository and push this folder to it.
2. In the repository, open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
3. After a minute the site is live at `https://<account>.github.io/<repo>/`.

Note: `404.html` uses root-relative links, so it looks right once the site is on its own domain. On a `github.io/<repo>/` preview only that page's styling is affected.

## Move the domain over

Do this once the GitHub Pages site looks right.

1. **Verify the domain on GitHub first.** In your GitHub account (or organisation) settings, open **Pages → Add a domain**, enter `fundersfounders.world`, and copy the TXT record it gives you. Add that TXT record at GoDaddy. This stops anyone else from claiming the domain on Pages.
2. **Set the custom domain on the repo.** In **Settings → Pages → Custom domain**, enter `www.fundersfounders.world` and save. GitHub commits a `CNAME` file to the repository for you.
3. **Change DNS at GoDaddy.** Lower the TTLs a day beforehand so the switch is quick, then:

   | Type | Host | Value |
   |---|---|---|
   | CNAME | `www` | `<account>.github.io` (replaces `ghs.googlehosted.com`) |
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | TXT | `_github-pages-challenge-<account>` | the verification value from step 1 |

   Remove the existing A records on `@` (the Google one and GoDaddy's forwarding ones). Once the apex points at GitHub, GitHub redirects `fundersfounders.world` to `www.fundersfounders.world` automatically.
4. **Turn on HTTPS.** After DNS propagates, tick **Enforce HTTPS** in Pages settings. The certificate can take up to an hour to issue.
5. **Unhook Google Sites.** In the Google Site's publish settings, remove the custom domain mapping. Leave the site published on its `sites.google.com` address for a few weeks as a fallback.
6. If the domain is registered in Google Search Console, submit the new sitemap. The property itself does not change.

## Credits

Content and imagery belong to Funders Founders World / Crowd Product.
