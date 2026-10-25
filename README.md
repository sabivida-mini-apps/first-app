<p><img src="https://raw.githubusercontent.com/sabivida-mini-apps/.github/main/assets/social-first-app.png" alt="SabiVida first app: a starter page and server that verify SabiVida sign-in." width="100%"></p>

# Your first SabiVida mini app

A template for a [SabiVida mini app](https://github.com/sabivida-mini-apps/partner-kit): a web page that opens inside SabiVida and a small server that verifies SabiVida's launch token. Click **Use this template** to start your own.

Prefer a framework? See [first-app-react](https://github.com/sabivida-mini-apps/first-app-react), [first-app-next](https://github.com/sabivida-mini-apps/first-app-next), [first-app-vue](https://github.com/sabivida-mini-apps/first-app-vue) and [first-app-solid](https://github.com/sabivida-mini-apps/first-app-solid).

## Try it without SabiVida

`npm install && npm run dev:mock`, then open http://localhost:4398. A local stand-in for SabiVida frames the app, signs a test member in and answers step suggestions. It's for development only.

## Run it

```sh
npm install
SABIVIDA_HOST=https://sabivida.com MINI_APP_ID=your-app-id npm start
```

It serves your app on `http://localhost:4319`:

- **Framing:** the page sends `Content-Security-Policy: frame-ancestors https://sabivida.com`, so only SabiVida can frame it.
- **`POST /session`:** verifies the launch token against `https://sabivida.com/api/mini-apps/jwks.json`. It checks the issuer, your app id as audience, the `sabivida-launch+jwt` type, EdDSA, the 60-second age, and that each token is used only once.
- **`public/app.js`:** signs the member in and suggests a plan step with `SabiVida.addTask`.

## Deploy to Cloudflare Workers

```sh
npm run deploy -- --host https://sabivida.com --app your-app-id
```

To test against SabiVida's staging, ask the SabiVida team for the staging public keys and add `--jwks '<keys JSON>'`. Staging sits behind an access gate, so the app then verifies against those keys and serves its own copy of the SDK.

## Files

| File | Role |
| --- | --- |
| `partner.mjs` | The app: static pages, framing policy, token verification |
| `server.mjs` | Node server |
| `worker.mjs`, `wrangler.jsonc`, `deploy.mjs` | Cloudflare Worker and its deploy |
| `public/` | The page, its script and a privacy page (replace it with yours) |

Guide, protocol and SDK reference: [sabivida-mini-apps/partner-kit](https://github.com/sabivida-mini-apps/partner-kit).
