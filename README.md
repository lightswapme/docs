# LightSwap Partner API Docs

Mintlify documentation for the public LightSwap Partner API.

## Local preview

Install the Mintlify CLI if needed:

```bash
npm i -g mint
```

Run the preview server from this directory:

```bash
mint dev
```

## Validation

Run these checks before publishing documentation changes:

```bash
mint validate
mint broken-links
```

## Content boundaries

- Keep these docs public and partner-facing.
- Do not document internal database tables, admin SQL, raw API key generation, or internal service names.
- Do not expose partner API keys in examples.
- Use `https://lightswap.me/api/partner/v1` as the production API base URL.
