# Directory submission

- **Name:** Notit
- **Permanent slug:** `notit`
- **Tagline:** Search your Notit study materials and read the sources with Claude.
- **Description:** Search across your Notit courses, lectures, Notes, Final Notes, and transcripts without choosing a course first. Read complete notes or original transcript passages, then get answers with links to the source in Notit. Note links keep the version found during search. You can also review summaries, keywords, exam points, and Quick Reviews. Access is read-only and limited to the permissions you approve. Requires a Notit account and a Plus or Pro plan to read study data.
- **Categories:** Education, Productivity
- **Documentation:** https://notit.ai/en/integrations/claude
- **Privacy policy:** https://notit.ai/en/privacy-policy
- **Support:** help@metaplad.com, https://notit.ai/en/help
- **Company:** METAPLAD Co., Ltd., https://notit.ai
- **Authentication:** `oauth_cimd`
- **Data source:** First-party API
- **Access:** Read-only
- **Health information:** None
- **Sponsored content:** None
- **Icon:** `assets/notit-icon-256.png` (existing square Notit logo; unchanged)

Reviewer credentials are not stored in this repository. They must be delivered only through Anthropic's submission portal.

## Version 1.1.0

The remote endpoint and OAuth scopes are unchanged. Add `search` and `fetch` to the directory tool list and refresh the captured server tools through the existing Claude connector. The five existing read permissions expose these 18 tools:

- `search`
- `fetch`
- `health`
- `list_courses`
- `get_course`
- `get_next_course`
- `list_lectures`
- `get_lecture`
- `list_studypacks`
- `get_studypack`
- `get_studypack_markdown`
- `get_studypack_quick_review`
- `search_studypack_content`
- `list_transcripts`
- `search_transcripts`
- `list_transcript_summaries`
- `list_transcript_keywords`
- `list_exam_points`

## Examples and review checks

- Ask: “Find my Notit materials about heat and work, read the matching sources, and explain the difference with source links.” Verify `search` runs without course or lecture IDs, `fetch` uses exact returned IDs, and the answer cites returned URLs.
- Repeat with Korean: “내 Notit 자료 전체에서 열과 일을 찾아 원문을 읽고, 출처 링크와 함께 차이를 설명해줘.” Also verify a query with no matching material returns an empty result set without invented sources.
- With matching Note and Final Note fixtures, verify whole Markdown, including tables, math, code, and images. Multiple matching blocks must produce one document result. Search selects the current version and the returned Note ID and source URL pin that version.
- With a matching transcript fixture, verify original text, language, start/end milliseconds, and the owning lecture's transcript link. Empty transcript results do not establish a successful transcript fetch.
- Open cited links while signed in to the same Notit account. A source URL must not enable public sharing.
- With only `note:read`, verify course, lecture, and transcript sources are excluded and direct fetches of those types are denied. With only `exam_point:read`, `search` and `fetch` are not listed.
- Check other-user IDs, deleted or inactive parents, unavailable sources, Free plan responses, and expired or revoked tokens. No unauthorized content should be returned.
- Confirm all tool titles have matching `annotations.title`, all tools remain read-only, and search/fetch expose explicit input/output schemas with identical JSON in `structuredContent` and text content.
- Exercise the existing tools to check for regressions. Record which live fixtures and Claude surfaces were actually tested; local protocol tests alone are not live Claude validation.

Published directory edits are reviewed before replacing the current public listing. Keep private reviewer credentials in Anthropic's portal, and do not add them to this file or the changelog.
