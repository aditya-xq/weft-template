# Weft — Quickstart Template

This repository is a **template** to onboard GitHub repositories to **Weft** (the daily GitHub summary action).

> 🧵 **Weft** collects GitHub activity, renders a visual summary, and (optionally) publishes it to X/Twitter.

---

## Quickstart — get a daily summary in 3 steps

1. Click **Use this template** → create a new repository for your account.
2. Add required repository **secrets** (see below).
3. Enable Actions and optionally edit `config/default.yml` to customize. The scheduled job will run automatically.

---

## Required repository secrets

Create these repository secrets (Repository settings → Secrets → Actions):

- `GITHUB_TOKEN` — (usually provided by GitHub automatically; keep it)
- `X_CONSUMER_KEY` — X/Twitter Consumer Key
- `X_CONSUMER_SECRET` — X/Twitter Consumer Secret
- `X_ACCESS_TOKEN` — X/Twitter Access Token
- `X_ACCESS_SECRET` — X/Twitter Access Secret

> If you only want to preview and not publish, use `config/dry-run.yml` (it sets `twitter.publish: false`).

---

## Workflow(s)

- `.github/workflows/daily-github.yml` — scheduled daily run (default 03:30 UTC).
- `.github/workflows/manual-run.yml` — manual workflow_dispatch for testing/preview.

By default, the workflows reference `aditya-xq/weft@main`.

---

## Customize the config

Open `config/default.yml` and update:

- `github.username` — set to your GitHub username.
- `runtime.timezone` — change if you're not in Asia/Kolkata.
- Visual theme values and `time_window.duration`.

Save and commit; the next run will use the updated config file.

---

## Dry runs & debugging

To preview output without publishing:

1. Run the **Manual / Preview: Weft** workflow from the Actions tab and choose `config/dry-run.yml`.
2. Or edit `config/default.yml` and set `twitter.publish: false`.

Dry run outputs are typically written to `out/summary.svg` & `out/summary.png` (see the project README in the action repo for exact locations).

---

## Advanced tips

- Pin the action to `aditya-xq/weft@main` for the latest release. When a new major is ready, release `v2` and update template changelog.
- If you prefer to use an organization-level repo, this template can be used as-is.
- For privacy, run with `twitter.publish: false` until you confirm visuals and metrics.

---

## Troubleshooting

If the action fails:
- Confirm secrets are set and valid.
- Use the manual run with `dry-run` config to generate artifacts without publishing.
- Check workflow logs for error messages; common issues are token permissions or wrong `github.username`.
