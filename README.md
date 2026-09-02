# Notit for Claude

Study your Notit classes with Claude. This plugin adds the official read-only Notit MCP connection to Claude without installing scripts, skills, commands, hooks, or agents.

## Install

When the plugin is available in the Claude directory, open Claude's plugin settings, find **Notit**, install it, and enable it. The plugin is disabled by default so that you explicitly choose when to connect your Notit account.

To test the public source directly with Claude Code:

```sh
git clone https://github.com/metaplad/notit-claude-plugin.git
claude --plugin-dir ./notit-claude-plugin
```

Open `/mcp` in Claude Code and authenticate the `notit` server. Claude opens Notit's OAuth consent page; no token or secret belongs in this repository or in `.mcp.json`.

The same remote endpoint can be added as a Claude custom connector:

```text
https://mcp.notit.ai/mcp
```

## Requirements

- A Notit account is required.
- OAuth connection is available on every Notit plan.
- Reading Notit data with the MCP tools requires Notit Plus or Pro. Free accounts receive Notit's existing upgrade-required response when a data tool is called.

## Read-only permissions

Notit shows the requested permissions before connecting. All are initially selected, and you can clear any permission as long as at least one remains.

| Permission | Data Claude can read |
| --- | --- |
| `course:read` | Course lists, course details, and next-course information |
| `lecture:read` | Lecture lists and lecture details |
| `note:read` | StudyPacks, complete Markdown notes, and search results within a StudyPack |
| `transcript:read` | Lecture transcripts, transcript search results, summaries, and keywords |
| `exam_point:read` | Exam points and StudyPack Quick Reviews |

Only tools covered by the permissions you approve are exposed. The connection cannot create, edit, or delete Notit data.

## Data handling

Notit serves data from its first-party API only after checking that the signed-in account owns the requested material. Claude receives data only when you ask it to use a Notit tool and only within your approved permissions.

OAuth access tokens expire after one hour. Rotating refresh tokens expire after up to 90 days and are revoked when you disconnect or when reuse is detected. Claude and Anthropic process data delivered to Claude under the terms, product settings, and retention policies applicable to your Claude account.

Read the [Notit Privacy Policy](https://notit.ai/en/privacy-policy) and [Claude connection documentation](https://notit.ai/en/integrations/claude) before connecting especially sensitive class content.

## Disconnect

In Notit, open **Me → Integrations → MCP settings → Connected apps** and select **Disconnect**. You can also remove Notit from Claude. Disconnecting the OAuth app does not disable or replace a separately issued manual Notit MCP token.

## Support

Email [help@metaplad.com](mailto:help@metaplad.com) or visit [Notit Support](https://notit.ai/en/help).

## License

[MIT](LICENSE) © METAPLAD Co., Ltd.
