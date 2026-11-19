# DeftPDF for Claude

![DeftPDF](assets/icon.png)

Use your DeftPDF account to compress PDFs, make scans searchable with OCR,
convert PDFs to editable Word documents, merge PDFs in order, and split or
extract selected pages. Original documents remain unchanged. Files are
processed by DeftPDF's hosted service using your existing account entitlements.

This repository contains only the client plugin, its skills, and documentation.
It does not contain the DeftPDF application, processing backend, credentials,
customer documents, or a local PDF engine.

## Availability

This is a directory submission candidate, not an approved Anthropic listing.
Private web uploads currently require an explicitly approved DeftPDF account.
Installing the plugin does not grant preview access, increase file limits, or
change your plan. Contact [support](https://mcp.deftpdf.com/support) if access is
unavailable. A public listing does not imply that every account is eligible for
private uploads.

Claude Code installation and the original-private-upload workflow have been
validated. Hosted Claude has separate connector acceptance. Cowork behavior has
not been independently validated; no native attachment export is claimed on any
surface. The directory's availability depends on its review and each client's
supported components.

## Install in Claude Code

Add the standalone marketplace and install the plugin:

```sh
claude plugin marketplace add Jameslin-9880/deftpdf-claude-plugin
claude plugin install deftpdf@sictec-deftpdf --scope user
```

Restart Claude Code. Run `/mcp`, select DeftPDF, and complete normal browser
OAuth with your existing DeftPDF account. No API key is needed. Run
`/deftpdf:setup` to check the connected account's display name. Claude Code may
reuse an existing manually configured connection to the same
`https://mcp.deftpdf.com/mcp` endpoint instead of loading a duplicate. Use that
selected connection's authentication controls and leave unrelated connections
unchanged.

If the plugin is approved for Anthropic's directory, users can instead install
it there. A directory installation can synchronize to Claude Code through the
same Claude account. Local marketplace availability and directory approval are
separate states.

## Process the original PDF

1. Sign into [private uploads](https://deftpdf.com/mcp/input) with the same
   DeftPDF account shown by the connector.
2. Select and upload the ORIGINAL PDF privately. Copy its complete descriptor.
3. In Claude Code, run `/deftpdf:pdf` with the operation and descriptor. For
   example: compress it with balanced quality, make it searchable in English or
   Spanish, convert it to Word, merge two or more descriptors in order, or split
   it with ranges `["2", "1"]`.
4. Wait for the existing job to complete, then open the exact returned download
   link in your browser and save the result. Check OCR/conversion layout before
   relying on it.

The current seven tools cannot upload a local path, a Claude sandbox path, or
bytes read from disk. The webpage step is an explicit original-file upload,
not native attachment transfer. Do not reconstruct an original from extracted
text or substitute a public example. If only a local file or attachment is
available, the plugin stops and explains the private-upload step.

Merge accepts 2–10 PDFs and preserves their requested order. One split range
returns a PDF; multiple ranges return a ZIP. The plugin submits once and polls
the returned handle, honors retry delays, and does not replace a pending or
uncertain task. Identical private-input requests reuse their original task for
24 hours. A repeated call returning a cached job is not a new processing run.

## Privacy and permissions

OAuth identifies the connected account and permits PDF processing and job
status checks. It does not expose billing, subscription management or the
account's document library. Passwords, server credentials and delegated website
credentials are not sent to the model. The plugin contains no hooks, scripts,
background uploader, package installer or local processing dependencies.

The selected original PDF and processing options are sent to DeftPDF. Word
conversion uses CloudConvert; OCR uses OCR.space. Cloudflare provides network
security/delivery and private temporary input/result storage. See the published
[Integration Privacy](https://mcp.deftpdf.com/privacy) supplement for the full
processing, diagnostic-storage, operational-record and subprocessor disclosures.

Private upload references expire after one hour. Expired inputs are eligible
for periodic cleanup, with active-job leases and retries; deletion is not
instantaneous. Output links are temporary signed capabilities and may expire
before a job handle. Do not put private descriptors, job handles or signed links
in public issues, source repositories or documentation. Stable account mappings,
operational records and backups have different retention from temporary files.
See [privacy and limits](references/privacy-and-limits.md).

Existing plan entitlements and shared service capacity limits apply. The plugin
has no checkout, purchase or upgrade tool. It does not provide permanent
redaction, password protection, signing, or document-library browsing.

## Updates, removal and support

For marketplace updates:

```sh
claude plugin update deftpdf@sictec-deftpdf
```

To remove only this plugin:

```sh
claude plugin uninstall deftpdf@sictec-deftpdf
```

Use the selected connection's authentication controls to revoke its OAuth grant
when desired. Removing the plugin does not cancel accepted jobs or disable
server-side input cleanup; unexpired result links remain independent.

- [Support](https://mcp.deftpdf.com/support)
- [Privacy policy](https://mcp.deftpdf.com/privacy)
- [Terms of service](https://deftpdf.com/terms)
- [Review cases](docs/REVIEW_CASES.md)
- [Release notes](CHANGELOG.md)

Published by Sictec Infotech Inc. Directory organization ownership and legal
acknowledgements are completed separately by the authorized company publisher.
