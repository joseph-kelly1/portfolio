# Deployment and Maintenance

Released on 2026-10-14 after Joseph authorized hosting and explicitly approved publishing both email addresses and the current project updates.

## Live site

- Portfolio: https://josephkelly.dev/
- Railway URL: https://portfolio-production-bfd6.up.railway.app/
- Railway project: `portfolio` (`5c8e57ef-c78e-48b6-98e4-513f6169b3ca`)
- Railway service: `portfolio` (`1253ddb9-8148-43fc-8d0b-eabeeb09ea30`)
- Production environment: `34ff5d48-d7f1-4e4e-9e5d-3149cee5ec54`
- Dashboard: https://railway.com/project/5c8e57ef-c78e-48b6-98e4-513f6169b3ca
- Repository: https://github.com/joseph-kelly1/portfolio, branch `main`

## Serving and runtime

Railway Railpack detects the root `Staticfile` and serves `public/` with Caddy. No application build, Node/Python runtime, package install, database, or application environment variables are required.

`Staticfile` sets `root: public` and `index_fallback: false`. Only that public directory is served. Source files under `resume/`, `docs/`, and `plans/` must remain outside it. The résumé PDF is no longer published; keep résumé files outside `public/`.

Railway service settings are configured on the platform:

| Setting | Value |
| --- | --- |
| Builder | Railpack |
| HTTP healthcheck | `/` |
| Healthcheck timeout | 60 seconds |
| Restart policy | On failure, maximum 3 retries |
| Region | us-west2, one replica |
| Custom start/build commands | None |
| Domain target port | Automatic detection |

No deprecated `railway.json` is required. New Railway services ignore that older format, so it was removed. The static build is controlled by `Staticfile`; healthchecks and restart settings are stored on the service.

## Updates

1. Preview changes locally: `python3 -m http.server 8000 --directory public`.
2. Commit and push to `main` when Joseph requests it. The Railway service is linked to `joseph-kelly1/portfolio` on that branch and deploys GitHub updates automatically.
3. Confirm a successful Railway deployment, then inspect https://josephkelly.dev/ and the changed assets.
4. Confirm the personal email and résumé links are absent and `/assets/resume-portfolio.pdf` returns 404.

Useful read-only checks:

```sh
railway deployment list --project 5c8e57ef-c78e-48b6-98e4-513f6169b3ca --service portfolio --environment production --limit 3
railway domain status josephkelly.dev --project 5c8e57ef-c78e-48b6-98e4-513f6169b3ca --service portfolio --environment production
```

Do not publish `plans/`; Git ignores it. Do not put account credentials or tokens in source.

## Cloudflare DNS

The apex CNAME is `josephkelly.dev` → `z9hg3jl0.up.railway.app`, proxied, TTL Auto. Railway ownership is verified by the TXT record at `_railway-verify.josephkelly.dev`. Its value is available in Railway's domain status and the Cloudflare dashboard.

The pre-existing Cloudflare Full TLS mode and proxying were preserved. Railway reports the apex domain active, ownership verified, and certificate valid.

Only the two old apex A records were replaced, and the apex verification TXT was added. NU Insights, its verification TXT, the other subdomains, existing NS records, and all other records were left unchanged. `www` remains on its previous destination; this release covers the requested apex domain only.

## Rollback

For a bad site update, use the Railway service's deployment history to roll back to a previous successful deployment, or revert the offending Git commit and push that revert to `main`. Do not change DNS for a normal content rollback.

To restore the exact pre-release apex DNS state:

1. Remove the portfolio apex CNAME.
2. Recreate these two A records with proxying enabled and TTL Auto:
   - `josephkelly.dev` → `44.227.65.245`
   - `josephkelly.dev` → `44.227.76.166`
3. Remove only the apex `_railway-verify.josephkelly.dev` TXT if disconnecting the portfolio. Preserve the separate `_railway-verify.nuinsights` record.

These were the old root destinations; restoring them restores the previous routing, not a prior portfolio version. A local backup is also in ignored `plans/dns-before-release.json`.

## Release verification

- Railway deployment succeeded; the direct Railway page, stylesheet, PDF, Sora font, Auto Lead screenshot, and source-path isolation were checked. Downloaded public files matched local files byte for byte.
- https://josephkelly.dev/ renders the portfolio in a browser with Sora and all three projects.
- All three project screenshots load, with no browser console errors observed.
- The resume downloaded through the custom-domain link matches the previously verified phone-free PDF byte for byte.
- No horizontal overflow at 320 or 1440 pixels; temporary viewport overrides were reset.
- Railway reports domain ownership verified and certificate status valid.
- NU Insights still responds over HTTPS with HTTP 200 and its original Railway CNAME.
- Non-public source paths return 404 on the Railway origin.
- The raw Python HTTP client received 403 from the proxied apex; custom-domain checks therefore used the real browser and its resume download. No Cloudflare security settings were weakened.

Safari, Firefox, real mobile hardware, and screen readers remain outside the recorded test coverage. Earlier QA evidence is in `docs/qa.md`.
