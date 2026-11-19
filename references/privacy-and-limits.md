# Privacy and limits

DeftPDF processes the original PDF on its hosted service. This plugin connects
to https://mcp.deftpdf.com/mcp using scoped browser OAuth. It contains no account
credentials, local PDF engine, background hooks, or automatic file uploader.

Private web uploads are authenticated, account-bound and temporary. They are
kept out of the document library and public file hosting. The upload page shows
their expiry. Accepted-job replay is retained for 24 hours; an expired input is
not a reason to resubmit an accepted job. Input pruning and one-day private
storage lifecycle rules bound retention, with active-job leases and cleanup
retry behavior. Results are temporary signed downloads, not permanent storage.

Private uploads currently require explicit account approval. Installing the
plugin does not enable this feature for an unapproved account. Existing account
entitlements, file-size/page limits and service capacity apply. The plugin does
not purchase plans or change subscriptions. CloudConvert remains the hosted
Word conversion provider. DeftPDF policies govern processing and subprocessors:

- [Privacy](https://mcp.deftpdf.com/privacy)
- [Support](https://mcp.deftpdf.com/support)
- [Terms](https://deftpdf.com/terms)

The seven remote tools support compression, searchable OCR, PDF-to-Word, ordered
merge, split/extraction, minimal account identification and job status. They do
not expose document-library access, billing history, redaction, encryption,
form signing, or direct original-byte upload from Claude Code. Reading a local
PDF in Claude Code does not upload it to the remote service.
