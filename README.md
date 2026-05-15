# claude-deeplink

Static helper to build `claude-cli://open?...` deeplinks for [Claude Code](https://code.claude.com/docs/en/deep-links).

**Live demo:** https://prespic.github.io/claude-deeplink/

Single HTML file. No build, no install. Open `index.html` locally or host on GitHub Pages.

## Features

- Form-driven URL builder with live preview
- Pick target: `repo` (Claude auto-finds local clone), `cwd` (absolute path), or none
- Copy URL or `<a href>` snippet
- "Open" button to test directly
- History stored in `localStorage` (last 20)
- Light / dark theme toggle
- Tailwind v4 browser + DaisyUI v5 via CDN, no build step

## Hosting on GitHub Pages

```bash
gh repo create prespic/claude-deeplink --public --source=. --remote=origin
git add . && git commit -m "init: deeplink builder"
git push -u origin main
gh repo edit --enable-pages --pages-branch=main --pages-path=/
```

Then visit `https://prespic.github.io/claude-deeplink/`.

## Reference behavior

| Parameter | Behavior |
|-----------|----------|
| `q`       | Prefilled prompt (literal text, max 5000 chars, `%0A` for newlines) |
| `repo`    | GitHub slug — Claude resolves to most-recently-used local clone |
| `cwd`     | Absolute path — wins over `repo` if both provided |
| (none)    | Opens Claude Code in home / last session directory |

The deeplink **only prefills** the prompt — Enter is required to send.
Slash commands (e.g. `/review`) work: paste into `q`, hit Enter in Claude Code.

## Known issues

- GitHub Markdown strips `claude-cli://` links from rendered READMEs / issues / PRs. Workaround: wrap the URL in a code block so users can copy-paste.
- Requires Claude Code v2.1.91+.
