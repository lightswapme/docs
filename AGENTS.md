# Documentation project instructions

- Do not commit or push; only the user does that.
- Check Git status before editing and preserve other agents' uncommitted changes. Recheck files that change concurrently.
- Research the affected pages and interfaces. Ask the user when public behavior, claims, security, access, or another material choice remains unclear; resolve routine editorial choices directly.
- Use external services only when the task needs them and access is available. Missing MCP or connector access does not block safe local work.
- Never publish or perform another irreversible external action without the user's explicit authorization for that action.

## Larger changes

- For cross-project interfaces, major documentation redesigns, or unresolved behavior, confirm a concise spec with scope, exclusions, acceptance criteria, and an end-to-end check. Routine multi-file edits do not need one.
- Implement in working increments and reassess the cause if repeated fixes fail. Review large or high-risk diffs for correctness and requirement gaps.

## About this project

- This is the public Mintlify documentation site for LightSwap integrations.
- Pages are MDX files with YAML frontmatter.
- Configuration lives in `docs.json`.
- Run `mint dev` to preview locally.

## Style preferences

- Use active voice and second person.
- Keep sentences concise.
- Use sentence case for headings.
- Do not use em dashes (—). Use commas, colons, parentheses, or split the sentence instead.
- Use code formatting for endpoint paths, headers, file names, commands, and literal values.
- Prefer Mintlify components such as `Card`, `CardGroup`, `Steps`, `Note`, `Tip`, and `Warning` when they make the page easier to scan.

## Content boundaries

- Keep docs public and integration-facing.
- Do not use internal business or audience labels in public-facing docs. Use integration, API access, team, user, customer, or business depending on context.
- Do not document internal database tables, admin SQL, raw API key generation, or internal service names.
- Do not mention specific swap route providers.
- Do not promise zero fees. Wallet, gas, and blockchain network costs are separate third-party costs.
- Do not document unavailable features as live. Webhooks, browser keys, refund endpoints, and per-request custom fees are not included in the MVP. The partner dashboard (Account → Business) is live: self-serve activation, flat 0.5% rate, $10 minimum claim, USDC payouts to the LightSwap account balance.
- Use `https://lightswap.me/api/partner/v1` as the public API base URL until the real API route changes.
- Keep the site framed as a LightSwap documentation hub, not as API-only docs.

## Qwen copywriting workflow

- GPT remains responsible for coding, implementation, research, references, verified interfaces, confirmed facts, and the writing brief. For new or substantially rewritten public documentation prose, headings, website content, marketing, SEO text, and localization, load the official `qwencloud-text` skill and follow `docs/qwen-copywriting.md`.
- Use exactly `qwen3.8-max` for copywriting. Do not silently substitute another model or write the prose with GPT if Qwen is unavailable.
- Ask Qwen for at least three complete, distinct, numbered variants for each requested content unit and locale. Keep multilingual variants aligned by number so the user can choose a coherent set.
- Save the original Qwen response and share its full wording and every returned variant with the user in the original order. GPT must not filter, omit, shorten, rewrite, translate, merge, rank, or preselect Qwen's text. Preserve additional variants if Qwen returns more than requested.
- Put factual, interface, MDX, locale, and length checks in separate notes outside Qwen's text. Corrections and stylistic revisions must come from Qwen; retain and expose the original response as well.
- Wait for the user's choice before inserting new prose into public pages, unless the user explicitly delegates selection. Integrate the selected wording verbatim; only serialization or markup escaping that preserves the rendered wording is allowed.
- Internal instructions, research notes, code examples, API contracts, schemas, configuration, and mechanical moves of already approved text remain GPT work. This exception does not allow GPT to author or edit public explanatory prose.

## Verification contract

- For instruction or internal-document changes only, run `git diff --check`.
- For public Mintlify pages or `docs.json`, run `mint validate` and `mint broken-links`, and fix failures caused by the change.
- Preview with `mint dev` when layout or components change.
- Report the commands run, their results, and any checks that could not run.
