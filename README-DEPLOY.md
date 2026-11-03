# Project Nightingale — passphrase-protected Vercel upload

Upload only the `project-nightingale/` folder. It contains two files:

- `index.html` — the CreditSwan gate page with the whole packet inside it, encrypted (AES-256-GCM; key derived from the
  passphrase with PBKDF2-SHA256, 400,000 iterations). The packet is decrypted in the reader's browser; nothing readable is
  served, cached or sent anywhere. A wrong passphrase simply fails to decrypt.
- `vercel.json` — static-site settings and headers: noindex, no-store, no-referrer, frame-ancestors none, and a content
  security policy that allows only the page's own script and Google Fonts.

Deploy:

    cd project-nightingale
    npx vercel --prod

or drop the two files into the `creditswan-brand` project's static root (or a sub-path such as `/nightingale/`) and push.
Nothing needs building. The page must be served over https (Vercel always is); Web Crypto is not available on plain http.

Readers enter the passphrase you set once per browser tab; a reload in the same tab reopens without asking. Share the
passphrase separately from the link. To change it, re-run the packaging step with a new passphrase — the passphrase is not
stored anywhere in these files.

Keep the unprotected copy (`project-nightingale-vercel.zip`, with the plain `index.html`) off any public host.
