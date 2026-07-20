# DSE Client Type Stats

A free, self-updating website showing **client-type Buy % / Sell %** on the Dhaka
Stock Exchange (Retail, Institution, Dealer, Foreign, Others), from the DSE
**Daily Market Snippet**. Look up any client type over a date range to see its
Net position (Buy − Sell) trend, plus a bar chart of the average Net position of
every client type over that window. Runs at **$0/month**.

- **Live site:** https://client-type-trade.jahid.ca
- **Sister site (block trades):** https://blocktrade.jahid.ca
- Password-protected (same access password as the block-trade site).

## How it works
Every trading day at 5:00 PM Dhaka time (11:00 UTC), GitHub Actions runs
`snippet_collector.py`. It downloads the Daily Market Snippet PDF, reads the
"Client Type Wise Statistics" table, and appends that day's Buy % / Sell % per
client type to `client_stats.json` (date-idempotent — no duplicates, weekends and
holidays self-skip). GitHub Pages then redeploys automatically. A visitor's
browser loads `client_stats.json` and computes the trend and averages on the fly.

## Files
- `index.html` — the website (password gate, filters, Net trend line, average bar chart, day-by-day table)
- `client_stats.json` — the accumulating data file (one row per trading day)
- `snippet_collector.py` — the daily fetcher/parser
- `.github/workflows/collect.yml` — the daily schedule
- `requirements.txt`, `CNAME`

Data source: Dhaka Stock Exchange — Daily Market Snippet (dsebd.org).
