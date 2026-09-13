# Send Artifact skill

Publish a static HTML page from any agent to a link you can share. The first
publish needs no account.

This repo holds one skill, `send-artifact`. Install it:

```bash
npx skills add SendArtifact/skill --skill send-artifact -g
```

Without npm:

```bash
mkdir -p ~/.claude/skills/send-artifact && \
  curl -fsSL https://sendartifact.com/skill.md -o ~/.claude/skills/send-artifact/SKILL.md
```

That path is Claude Code's. Any agent that loads SKILL.md files can keep the
same file wherever it looks for skills; the commands in it are identical.

## Publish now (no account)

One request. Send the HTML as the body and read the two links back:

```bash
curl -sS -X POST https://sendartifact.com/v1/publish \
  -H 'content-type: text/html' --data-binary @index.html
```

Returns `{url, claimUrl, expiresAt}`. The `url` is the page. The `claimUrl` is
private: it moves the page to an account and keeps it past the 7-day expiry.
With an account, tell your agent to publish to sendartifact.com with your
account instead, and the page gets a permanent address, access control, reader
analytics, comments, and versions with rollback.

## Generated, never edited

`skills/send-artifact/SKILL.md` is a copy of
<https://sendartifact.com/skill.md>, pulled every six hours by
[`.github/workflows/sync.yml`](.github/workflows/sync.yml). The served file is
the canonical one: a change made here is overwritten by the next sync.

## More

- Full agent manual: <https://sendartifact.com/llms.txt>
- Human walkthrough: <https://sendartifact.com/getting-started>
- Questions: support@sendartifact.com

MIT licensed — see [LICENSE](LICENSE).
