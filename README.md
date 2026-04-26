# LightSwap Documentation

Mintlify documentation for the public LightSwap integration site.

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

- Keep these docs public and integration-facing.
- Do not document internal database tables, admin SQL, raw API key generation, or internal service names.
- Do not expose API keys in examples.
- Use `https://lightswap.me/api/partner/v1` as the production API base URL.
- Do not present planned integrations as live features.
