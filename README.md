# Letta Docs Markdown Mirror

This repository is an automatically generated, grep-ready Markdown mirror of
[docs.letta.com](https://docs.letta.com).

Start with [`llms.txt`](./llms.txt) for the documentation map, then read the
relevant `index.md` files. The generated API reference is under `api/`.

## Why there is only one commit

This repository intentionally has no version history. Every publication creates
a new root commit and force-pushes it to `main`, so a fresh clone contains only
the current documentation snapshot and one commit.

This is expected. Do not try to merge or rebase an existing checkout after an
update. Either clone the repository again, or replace the checkout with the
latest snapshot:

```sh
git fetch origin
git reset --hard origin/main
```

**Do not edit this repository by hand or open pull requests.** Changes are
replaced by the next successful docs publication.
