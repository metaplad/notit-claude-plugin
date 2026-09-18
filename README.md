# Notit for Claude

Search your Notit study materials, read the sources, and get answers with source links in Claude. This plugin adds the official read-only Notit MCP connection to Claude without installing scripts, skills, commands, hooks, or agents.

## Install

Open the [Notit listing in the Claude directory](https://claude.ai/directory/notit) and connect your account. For the Claude Code plugin, install and enable **Notit** through your plugin settings or use the source installation below. The plugin is disabled by default so that you explicitly choose when to connect your Notit account.

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

## Search, read, and cite

Ask about a topic without choosing a course or lecture first:

1. `search({ query })` searches course and lecture titles, current Notes and Final Notes, and transcript utterances across your account. It returns up to 20 document references with `id`, `title`, and `url`.
2. `fetch({ id })` reads the exact returned ID and supplies the source text and URL. Notes and Final Notes return complete Markdown; transcript results return the matching original utterance, language, and millisecond time range. Courses and lectures return basic information only.
3. Ask Claude to answer from the fetched sources and cite their returned Notit URLs. Open a source link while signed in to the same Notit account.

Note results are deduplicated by document and retain the version found during search in their IDs and URLs. Searching selects the current version; fetching an earlier result preserves that result's version even after a newer version is created. Source links do not enable public sharing.

Example requests:

- “Find my Notit materials about heat and work, read the matching sources, and explain the difference with source links.”
- “Search my Notes and Final Notes for arithmetic and geometric means, then explain the key formulas with citations.”
- “Find a transcript passage about consumer behavior and show the original wording, language, time range, and source link.”
- “내 Notit 자료 전체에서 열과 일을 찾아 원문을 읽고, 출처 링크와 함께 차이를 설명해줘.”

Existing tools for courses, lectures, StudyPacks, transcripts, summaries, keywords, exam points, and Quick Reviews remain available. All five permissions expose 18 tools including `health`, `search`, and `fetch`.

## Read-only permissions

Notit shows the requested permissions before connecting. All are initially selected, and you can clear any permission as long as at least one remains.

| Permission | Data Claude can read |
| --- | --- |
| `course:read` | Course title search, course lists, course details, and next-course information |
| `lecture:read` | Lecture title search, lecture lists, and lecture details |
| `note:read` | Notes, Final Notes, complete Markdown, account-wide note search, and StudyPack tools |
| `transcript:read` | Original transcript utterances and timing, account-wide and lecture-specific search, summaries, and keywords |
| `exam_point:read` | Exam points and StudyPack Quick Reviews |

Only tools covered by the permissions you approve are exposed. `search` and `fetch` are available with at least one of `course:read`, `lecture:read`, `note:read`, or `transcript:read`; `exam_point:read` alone does not expose them. Search filters data types by your permissions, and every fetch rechecks ownership, permissions, active parent relationships, and source availability. No new OAuth permissions are needed for version 1.1.0. The connection cannot create, edit, or delete Notit data.

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
