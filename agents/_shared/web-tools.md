# Web Tools — Fetch Patterns for All Agents

Quick reference for reliably fetching content from sources that block direct access.

---

## Twitter / X Posts

X.com blocks unauthenticated fetches. Use the **FxTwitter API** instead:

```
Replace: https://x.com/{user}/status/{id}
With:    https://api.fxtwitter.com/{user}/status/{id}
```

Returns clean JSON with full tweet text, author, media, and metrics. No auth required. Works for all public tweets.

**Example:**
- Original: `https://x.com/godofprompt/status/2041265656893489419`
- Fetch as: `https://api.fxtwitter.com/godofprompt/status/2041265656893489419`

**When someone sends you an X link**, automatically convert it to the api.fxtwitter.com format before fetching.

---

## Paywalled Articles (Substack, Medium, etc.)

Try appending `?utm_source=pocket_saves` or fetching the plain reader URL if available. If still blocked, ask Artem to paste the text directly.

---

## GitHub

Use the `gh` CLI for GitHub content — PRs, issues, code:
```
gh pr view <number> --repo owner/repo
gh issue view <number> --repo owner/repo
gh api repos/owner/repo/contents/path/to/file
```

Prefer `gh` over WebFetch for GitHub URLs — it's authenticated and more reliable.

---

## General Notes

- Always note the source URL and access date when collecting research artifacts
- For real-time data (prices, metrics, live stats), flag the timestamp — these go stale fast
- If a fetch fails, try the cached/archive version via `https://webcache.googleusercontent.com/search?q=cache:{url}`
