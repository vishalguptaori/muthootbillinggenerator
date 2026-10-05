# Muthoot Billing Generator

A single-file, browser-based tool that turns raw voice-bot call reports into an
invoice working file. Open `muthoot-billing-generator.html` in any browser — no
install, no server, no build step.

## What it does

- Reads call reports as `.csv`, `.xlsx` or `.xls` (CSV is streamed, so file size is unlimited)
- Bills on minute pulses: `floor(seconds / 60) + 1`
- Splits Hindi and regional by keywords in the bot name
- Excludes test calls, duplicate call IDs, RNR calls over a set duration, and calls with no LOB mapped
- Produces an Excel working file with these sheets:
  - **Invoice Working** — the billable summary, costs as live formulas
  - **Day-wise** — pulses and cost per calling day
  - **Summary** — every rule applied in the run, for audit
  - **Bot-wise** — per-bot volumes
  - **Skipped calls** — every excluded row with its reason
- Produces a separate Product Summary (LOB × campaign type) workbook

## Rates

Rate fields ship **blank by design** — no pricing is stored in this repository.
Enter the Hindi and regional rates before generating; the tool refuses to run
without them rather than silently producing a zero invoice.

## Privacy

All processing happens in the browser. No call data, customer data or rate
information is uploaded anywhere. Nothing is written to disk except the files
you explicitly download.

Do not commit call reports, allocation files or generated invoices to this
repository — see `.gitignore`.
