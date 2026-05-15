# GCP OAuth Client Update — jetblip.com

**Date:** 2026-05-15
**Project:** labs (labs-jeremy)
**Client:** aijetlabs-labs
**Client ID:** 152013077104-qged7rqqqsecm6ghbck4ojao9h571bup.apps.googleusercontent.com

## Change

Added `my.jetblip.com` entries to the OAuth 2.0 client to support Google login on the new domain.

### Authorized JavaScript Origins — added
- `https://my.jetblip.com`

### Authorized Redirect URIs — added
- `https://my.jetblip.com/auth/google/callback`

### Existing entries preserved
- `https://my.aijetlabs.com/auth/google/callback`

## Verification

Settings saved via Google Cloud Console (OAuth client saved toast confirmed).
Reload of client page confirmed both new entries persisted.

Note: Google warns that settings may take 5 minutes to a few hours to take effect.
