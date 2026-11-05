# Release the Gemini CLI extension and Antigravity plugin

## Validate a candidate

From the parent directory:

```bash
gemini extensions validate ./compteam-gemini-extension
gemini extensions link ./compteam-gemini-extension
```

For Antigravity, run `agy plugin validate --strict .` from the repository root (0 errors and 0 warnings), then `agy plugin install .` and `agy inspect`.

Restart Gemini CLI or Antigravity and verify public club search, schedules, prices, and branch details. Run `/mcp auth compteam`, complete the browser sign-in, then verify `connect_compteam_account`, `list_my_subjects`, `list_my_classes`, and `get_account_status` with an authorized test account. Test RSVP and trial inquiries only with a suitable test account and explicit confirmation of those changes. Validation checks structure only; it does not establish that OAuth or the live tools work.

## Production authentication setup

Created and read back on 2026-11-05:

| Setting | Value |
| --- | --- |
| Supabase OAuth app | **Compteam for Gemini CLI (extension)** |
| Public client ID | `9d6b8c8d-6f77-4073-962c-69b11fb7456e` |
| Exact callback | `http://localhost:38762/oauth/callback` |
| Client type | Public, token endpoint authentication `none`, no secret |
| Compteam client registration | Active, `marketplace_safe`, audience `https://api.compteam.io/mcp` |

| Setting | Antigravity |
| --- | --- |
| Supabase OAuth app | **Compteam for Antigravity (plugin)** |
| Public client ID | `dc9dd148-1dae-4cc6-918b-cc257341fc4c` |
| Exact callback | `https://antigravity.google/oauth-callback` |
| Client type | Public, token endpoint authentication `none`, no secret |
| Compteam client registration | Active, `marketplace_safe`, audience `https://api.compteam.io/mcp` |

The Gemini CLI authorization endpoint accepts only its exact callback; any other port returns `400 invalid redirect_uri`. Keep `redirectUri` pinned in `gemini-extension.json`. The Supabase auth server does not offer dynamic client registration, so Gemini CLI cannot register its own client. Do not reuse the Claude client IDs here.

Do not put service-role keys, user tokens, reviewer passwords, or client secrets in this public repository.

## List in the extension gallery

The [Gemini CLI extension gallery](https://geminicli.com/extensions/) indexes public repositories automatically; there is no submission form.

1. Keep the repository public with `gemini-extension.json` at the root.
2. Add the GitHub topic `gemini-cli-extension` to the repository's About section.
3. The crawler checks tagged repositories daily. The extension appears once it passes validation.

Gemini CLI was replaced by Antigravity CLI for unpaid-tier and Google One users on 2026-06-18. Antigravity does not read Gemini extensions directly; it loads `.antigravity-plugin/plugin.json` and `mcp_config.json` from this repository.

## Submit to the Antigravity Marketplace

1. Pass `agy plugin validate --strict` with no errors or warnings.
2. Keep `name`, `displayName`, `description`, `version`, `logo`, `suggestedPrompts`, and `author` complete in `.antigravity-plugin/plugin.json`, with the bundled `assets/icon.png`.
3. Submit through Google's partner intake form linked from the Antigravity "Build plugins" documentation.

## Release an update

1. Increase `version` in both `gemini-extension.json` and `.antigravity-plugin/plugin.json` and update the documentation for the final behavior.
2. Validate, test the changed workflows, and commit.
3. Push to `main` and tag the release, for example `v0.1.1`. Users with `--auto-update` receive it on their next update check.
