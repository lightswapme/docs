# Documentation project instructions

## About this project

- This is the public Mintlify documentation site for LightSwap Partners.
- Pages are MDX files with YAML frontmatter.
- Configuration lives in `docs.json`.
- Run `mint dev` to preview locally.
- Run `mint validate` and `mint broken-links` before publishing changes.

## Style preferences

- Use active voice and second person.
- Keep sentences concise.
- Use sentence case for headings.
- Use code formatting for endpoint paths, headers, file names, commands, and literal values.
- Prefer Mintlify components such as `Card`, `CardGroup`, `Steps`, `Note`, `Tip`, and `Warning` when they make the page easier to scan.

## Content boundaries

- Keep docs public and partner-facing.
- Do not document internal database tables, admin SQL, raw API key generation, or internal service names.
- Do not mention specific swap route providers.
- Do not promise zero fees. Wallet, gas, and blockchain network costs are separate third-party costs.
- Do not document unavailable features as live. Webhooks, browser keys, public dashboards, refund endpoints, and per-request custom fees are not included in the MVP.
- Use `https://lightswap.me/api/partner/v1` as the public API base URL.
- Keep the site framed as a LightSwap Partners docs hub, not as API-only docs.
