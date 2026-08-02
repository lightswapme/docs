# Contribute to the documentation

Thanks for helping improve the LightSwap docs.

## Local development

1. Clone this repository.
2. Install the Mintlify CLI: `npm i -g mint`.
3. Run `mint dev` from the repo root.
4. Preview at `http://localhost:3000`.

Before opening a pull request, run `mint validate` and `mint broken-links` and make sure both pass.

## Writing guidelines

- Use active voice and second person: "Run the command", "you".
- Keep sentences short. One idea per sentence.
- Plain statements over metaphors. No hype words: seamless, effortless, unlock, empower.
- Don't use em dashes. Commas, periods, or colons instead.
- Use sentence case for headings.
- Use code formatting for endpoint paths, headers, file names, commands, and literal values.
- Prefer Mintlify components (`Card`, `CardGroup`, `Steps`, `Note`, `Tip`, `Warning`) when they make a page easier to scan.
- Don't hardcode specific asset lists, exact token or network counts, or APY numbers. The app shows live values. Rounded marketing claims (like "1,000+ assets") follow the app's own public copy.
- Content boundaries live in `AGENTS.md`. Read them before adding pages.
