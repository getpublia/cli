# Publia CLI

Command line client for Publia.

Publia CLI uploads webpages, Markdown files, and images to Publia and returns public preview URLs. It defaults to:

```text
https://getpublia.com
```

## Install

```bash
npm install -g publia-cli
```

Verify:

```bash
publia --help
publia commands --json
```

## Login

Use browser OAuth:

```bash
publia auth login
publia auth whoami --json
```

For non-interactive agents, issue a token from the Publia web UI and export it. The default server is already `https://getpublia.com`, so `PUBLIA_URL` is only needed for a different server.

```bash
export PUBLIA_TOKEN=publia_xxx
publia auth whoami --json
```

## Commands

```bash
publia ls [path] --json
publia cd <path>
publia open <path> --json
publia upload <file-or-dir> --json
```

Uploads fail on conflicts by default. Use `--rename` or `--overwrite` when that is intentional.

Local directory uploads skip symbolic links and hidden files/directories. The CLI only uploads supported Markdown, webpage, and image files, and it enforces the same safety limits as the server: maximum directory depth, maximum file count, maximum single-file size, and maximum total upload size.

## Agent Output

Agent-facing commands support a stable JSON envelope:

```json
{
  "ok": true,
  "data": {},
  "summary": "1 uploaded",
  "breadcrumbs": [
    { "action": "open", "cmd": "publia open /site/index.html --json" }
  ]
}
```

Use `--json --quiet` to print only `data`.
