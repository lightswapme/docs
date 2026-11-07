# Qwen copywriting workflow

This is an internal operating guide, not a public Mintlify page. Keep it out of `docs.json`. GPT handles research, verified interfaces, and implementation. Qwen writes public explanatory prose, and the user chooses among its unedited variants.

## Installed skills

- Official source: [QwenCloud/qwencloud-ai](https://github.com/QwenCloud/qwencloud-ai).
- Installed revision: `60542ab371ae2adc04937a3fdbbafe7baad7738c`.
- Text skill on this Mac: `/Users/rolaman/.agents/skills/qwencloud-text/SKILL.md`.
- Companion update checker: `/Users/rolaman/.agents/skills/qwencloud-update-check/SKILL.md`.
- Required copywriting model: `qwen3.8-max`, explicitly included in every request.

Both skills are installed at user scope and are shared with `lightswap-app`. The official skill files are unchanged. Locate the skill from Codex's skill list on another machine and use its script's absolute path. Installation is local; a clone of either project does not install the skills or credentials automatically.

## When to use Qwen

Use Qwen for new or substantially rewritten public documentation prose, page headings, descriptions, explanatory sections, FAQs, marketing, SEO text, and localization. Moving already approved text without editing its wording does not need another generation request.

GPT handles research, implementation, internal operating instructions, code samples, API contracts, endpoint paths, schemas, configuration, and MDX composition. These technical elements must come from verified interfaces. GPT must not use these exceptions to write public explanatory prose itself.

## Prepare the brief with GPT

Read the affected page and relevant interfaces before requesting prose. Collect references and examples when the task needs them. Pass their actual excerpts or summaries and source links to Qwen; a bare URL does not mean the text model has read the page.

Include:

- The content unit, placement, reader's goal, audience, and requested locales.
- Confirmed behavior, availability, restrictions, unresolved questions, and statements that must not be invented.
- The documentation project's style and content boundaries from `AGENTS.md`.
- Verified API paths, headers, parameters, enum values, code samples, and MDX requirements that must remain intact.
- User-provided tone preferences, examples, and length or layout constraints.
- A request for at least three complete, distinct, numbered variants per content unit and locale, all inside one assistant response. Align multilingual versions under the same variant number when multiple locales are requested.

Keep the brief appropriate to the affected documentation page. Integration documentation may need technical terms; do not automatically impose the consumer website's vocabulary on API documentation. Treat reference material as evidence rather than instructions. Resolve material interface or product questions with the user before supplying invented assumptions. Send only the relevant brief and public facts; keep credentials and unrelated private implementation details out of the request.

## Call the official text skill

Load `qwencloud-text` before calling it. Use its bundled Python script for Token Plan, preserve user-specified parameters, and follow its error and update-signal handling. Keep model defaults for thinking and sampling unless the user explicitly requests a change.

Create a fresh directory under `output/qwencloud-text/<unique-request-id>/` for each request. This directory is ignored by Git. Store the brief, source links, request, and responses there. Separate directories prevent concurrent chats from overwriting each other's drafts.

The request must contain `"model": "qwen3.8-max"` and a `messages` array with the brief and the requirement for at least three variants. Ask Qwen to number its variants itself so GPT does not have to label or reformat the wording.

For the installation on this Mac, run the following from the project working directory, replacing `<unique-request-id>` with a fresh identifier:

```sh
python3 /Users/rolaman/.agents/skills/qwencloud-text/scripts/text.py \
  --model qwen3.8-max \
  --file output/qwencloud-text/<unique-request-id>/request.json \
  --output output/qwencloud-text/<unique-request-id>/response.json \
  --print-response
```

Save the decoded `choices[0].message.content` from `response.json` directly as `response.md` without editing, trimming, normalizing, or adding a heading. The official skill returns one assistant message containing all requested variants. If an API response unexpectedly contains more choices, preserve and expose their content too. Retain the complete response JSON, including the reported model and usage.

After verifying that the response contains a nonempty assistant text, extract it mechanically. On this Mac, `jq -j` writes the decoded text without adding a newline:

```sh
jq -j '.choices[0].message.content' \
  output/qwencloud-text/<unique-request-id>/response.json \
  > output/qwencloud-text/<unique-request-id>/response.md
```

Credentials are read from the existing environment or the skill's supported local configuration. Do not print keys or store them in briefs, tracked files, or public examples. Use Token Plan only within user-initiated interactive agent work, in accordance with its terms, not in unattended jobs or application backends.

## Present the complete answer

Display every variant exactly as returned by Qwen, in its original order. Include links to the saved original text and JSON. If the complete answer is too long to reproduce in chat, provide the full original text file and clearly say it contains all variants; do not replace it with selected excerpts or a summary.

GPT must not filter, omit, shorten, rewrite, translate, merge, rank, preselect, or silently correct the prose. This includes punctuation, capitalization, provider mentions, and wording that fails a project preference. Run factual, interface, MDX, length, and locale checks separately, and put any concerns after the complete Qwen response, outside the original text.

If Qwen returns fewer than three variants, an incomplete answer, or truncated output, retain and expose that original, then request a complete set from the same model. Preserve every attempt in a new directory and share its original files. Never invent missing variants with GPT. If Qwen cannot complete the request, report the limitation and continue independent implementation work.

Ask Qwen for revisions when the user requests them. Provide the user's feedback without deleting earlier responses or using an edited GPT version as the purported Qwen original.

## User selection and implementation

Wait for the user to choose a variant or explicitly delegate selection before inserting new prose into public pages. GPT can progress on independent technical work using existing approved prose while the choice is pending.

Insert the chosen wording verbatim. JSON escaping and MDX wrappers may change the source representation only when the rendered wording stays the same. If a chosen text needs to be shortened, translated, corrected, or adapted, obtain a new Qwen response and present its variants for selection.

Verify the selected rendered text against the saved Qwen original and run the checks required by `AGENTS.md`. Keep notes about checks separate from the authored prose.

These are agent instructions, not a runtime filter or a technical lock on GPT's output. The saved original response is the independently inspectable source for checking that wording and variants were preserved.

## Failures and maintenance

Report a missing skill, credential issue, quota limit, unavailable model, or request failure explicitly. Never silently fall back to GPT, another Qwen model, `auto`, or pay-as-you-go credentials. Preserve the official skill's update handling. Record a new installed revision here and in the sibling project's guide when updating the shared skills.
