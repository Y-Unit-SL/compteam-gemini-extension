# Compteam — BJJ Classes & Memberships for Gemini CLI and Antigravity

Find Brazilian jiu-jitsu (BJJ) and martial arts clubs, explore class schedules, and compare membership plans and prices. Connect your Compteam account to view upcoming classes, check membership and payment status, and manage attendance for yourself or a linked child. You can also ask a club about an eligible free trial class.

## Release status

This is a preview extension. The production OAuth client, its callback, and the token audience were verified on 2026-11-05. In Antigravity CLI, Compteam sign-in and protected MCP tool calls were confirmed on 2026-11-05. Gemini CLI loads the extension and connects to the server; its account sign-in has not yet been exercised end to end. This extension is not affiliated with or endorsed by Google.

## What is included

- A remote MCP connection to `https://api.compteam.io/mcp`.
- The `compteam-training` skill for finding classes and plans, checking linked account information, and managing attendance.
- `rules/compteam.md` context with usage and safety guidance, loaded by both Gemini CLI and Antigravity.
- An Antigravity plugin manifest (`.antigravity-plugin/plugin.json`) and MCP configuration (`mcp_config.json`).

Public club details, schedules, and membership prices can be read without signing in. Personal information requires Compteam OAuth and is restricted to the signed-in person and children linked to that account. Attendance changes and trial inquiries require confirmation. Membership purchases, payments, club administration, and athlete registration are outside this extension's capabilities.

## Install in Gemini CLI

```bash
gemini extensions install https://github.com/Y-Unit-SL/compteam-gemini-extension
```

Restart Gemini CLI, then ask a relevant question. For personal features, run `/mcp auth compteam` and sign in on Compteam's consent page in your browser.

The extension configures a public OAuth client with the fixed callback `http://localhost:38762/oauth/callback`. There is no client secret in the extension. If that port is occupied, close the application using it and retry authentication. Sign-in needs a local browser that can reach the callback, so it does not work in headless sessions, remote SSH without forwarding, or most containers.

For local development:

```bash
gemini extensions link ./compteam-gemini-extension
```

## Install in Antigravity CLI

```bash
agy plugin install https://github.com/Y-Unit-SL/compteam-gemini-extension
```

Run `agy inspect` to confirm the plugin and its `compteam_compteam` MCP server loaded. When a personal tool needs your account, Antigravity opens Compteam's consent page in your browser. After you approve, the browser lands on `https://antigravity.google/oauth-callback`; complete sign-in as Antigravity prompts. The plugin uses its own public OAuth client and no client secret.

If you previously installed the Gemini CLI extension, `agy plugin import gemini` also registers it, but the Gemini manifest's loopback callback is not registered for Antigravity. Install the plugin from this repository instead.

## Try asking

- Find the Compteam club named ZR Team Andorra.
- Show this club's BJJ classes next week.
- What membership plans and prices does this club offer?
- Show my upcoming Compteam classes.
- Check my child's membership status.
- Help me confirm attendance for Thursday's BJJ class.
- Ask this club about a free trial.

Club discovery searches participating clubs by name. It is not a complete geographic search of every martial arts club. Class places, prices, eligibility, and account access come from live server responses.

## Privacy and data handling

The extension sends the arguments needed for each requested operation to the Compteam MCP server. Public searches send club names, branch identifiers, and requested weeks. After OAuth connection, personal tools use the authorized account to read limited membership, payment-status, and class information for the member or a linked child. Attendance changes send the selected class and intended RSVP. A trial inquiry sends the details the user supplies to Compteam for the selected club to handle.

The extension contains no local executable, hook, analytics collector, or credential file. Gemini CLI stores the OAuth tokens it obtains on your machine; Google's terms govern how Gemini processes your conversations. Compteam processes and retains server-side account and inquiry data under its [privacy policy](https://compteam.io/privacy). Follow that policy's contact and deletion-request instructions for Compteam data, and uninstall the extension or clear its MCP credentials to stop future access.

Linked-child features are for authorized parents or guardians. This training-management extension does not provide medical or fitness-safety advice. Do not put passwords, OAuth codes, payment credentials, or identity documents in the conversation.

## Documentation and support

- [Compteam MCP guide](https://compteam.io/documentation/mcp)
- [Support](https://compteam.io/documentation/support)
- [Privacy policy](https://compteam.io/privacy)
- [Terms of service](https://compteam.io/terms)
- Contact: [info@compteam.io](mailto:info@compteam.io)

## License and releases

Distributed under the [Unlicense](LICENSE). Compteam service access is governed by its terms of service.

See [the release guide](docs/RELEASING.md) for validation and gallery listing.
