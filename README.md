# Visoria AI — website

Marketing site and legal pages for the Visoria AI app, hosted on **Firebase Hosting**.

```
public/            # everything that gets deployed
  index.html       # landing page
  privacy.html     # served at /privacy
  terms.html       # served at /terms
  404.html
  assets/          # site.css, site.js, logo.svg
firebase.json      # hosting config (clean URLs, headers, caching)
.firebaserc        # Firebase project ID
```

## Local preview

```bash
npm i -g firebase-tools
firebase emulators:start --only hosting --project demo-visoria
# → http://127.0.0.1:5000
```

## Deploy

Manual:

```bash
firebase login
firebase deploy --only hosting
```

Automatic (GitHub Actions):

- `.github/workflows/firebase-hosting-merge.yml` deploys to the live channel on every push to `main`.
- `.github/workflows/firebase-hosting-pull-request.yml` deploys a 7-day preview channel for each PR and comments the URL.

Both need a repository secret named `FIREBASE_SERVICE_ACCOUNT` containing a service-account JSON key.
`firebase init hosting:github` creates the service account and the secret for you (rename the secret it creates, or update the workflows to match).

## GitHub Pages transition

The root-level `index.html`, `privacy.html` and `terms.html` are redirect stubs that send old GitHub Pages
visitors to the Firebase site.
Once the App Store / Google Play listings point to the new URLs, GitHub Pages can be disabled and these root files deleted.
