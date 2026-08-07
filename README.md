# SnapOtter LazyCat App

LazyCat LPK v2 packaging for [SnapOtter](https://github.com/snapotter-hq/SnapOtter).

This package uses `snapotter/snapotter:2.2.0` in single-container embedded mode. Per the SnapOtter 2.2.0 documentation, embedded mode is enabled by leaving both `DATABASE_URL` and `REDIS_URL` unset; SnapOtter then starts its own PostgreSQL 17 and Redis inside the container and stores data under `/data`.

The GitHub Action uses `snapotter/snapotter` as the version source and follows stable SemVer tags. The initial manifest is pinned to `snapotter/snapotter:2.2.0`.

## Build

```bash
lzc-cli project release -o dist/community.lazycat.app.snapotter.lpk
```

## OIDC

The manifest enables SnapOtter OIDC and maps LazyCat-provided OIDC values:

- `LAZYCAT_AUTH_OIDC_ISSUER_URI` -> `OIDC_ISSUER_URL`
- `LAZYCAT_AUTH_OIDC_CLIENT_ID` -> `OIDC_CLIENT_ID`
- `LAZYCAT_AUTH_OIDC_CLIENT_SECRET` -> `OIDC_CLIENT_SECRET`

SnapOtter callback path: `/api/auth/oidc/callback`.

The setup wizard also asks for a local fallback admin username and password. OIDC is the preferred login path, but the local account remains available if the identity provider is unavailable.

## GitHub Actions

Publishing uses `ca-x/lazycat-github-action/.github/workflows/lazycat.yml@v1`.

Required secrets for dual-store publication:

- `LZC_API_TOKEN`
- `APPSTORE_URL`
- `APPSTORE_TOKEN`

Optional secrets:

- `LZC_API_HOST`
- `LAZYCAT_TOKEN`
- `APP_ID`
- `PRIVATE_STORE_GROUP_CODES`
