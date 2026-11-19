# Reproducible review cases

Use synthetic PDFs only. A connected DeftPDF account must have the required
existing entitlements and, for private uploads, explicit preview access. Use a
dedicated reviewer account provided through the directory's secure access
channel. Never publish its password, callback, descriptors, handles or tickets.
Do not use an ordinary customer's paid account as a reviewer login.

## Setup

1. Install the plugin or add `https://mcp.deftpdf.com/mcp` as a custom connector.
2. Complete OAuth, call `get_deftpdf_account`, and confirm the intended reviewer
   display name. This tool returns a minimal opaque ID and name, not billing or
   library data.
3. Obtain the existing public synthetic originals from the links below. Upload
   the originals at `https://deftpdf.com/mcp/input` while signed in as the same
   account, then supply their complete descriptors unchanged.
4. Submit each requested operation once and use `get_deftpdf_job_status` with
   the returned job ID and operation. Keep all private values out of review notes
   and public recordings. Open results in the normal browser and inspect bytes.

| Synthetic original | Existing public source |
| --- | --- |
| image-heavy.pdf | https://deftpdf.com/uploads/mcp-review-v0.1/image-heavy.pdf |
| english-scan.pdf | https://deftpdf.com/uploads/mcp-review-v0.1/english-scan.pdf |
| spanish-scan.pdf | https://deftpdf.com/uploads/mcp-review-v0.1/spanish-scan.pdf |
| text.pdf | https://deftpdf.com/uploads/mcp-review-v0.1/text.pdf |
| two-pages.pdf | https://deftpdf.com/uploads/mcp-review-v0.1.1/two-pages.pdf |

## Five positive cases

| Case and natural prompt | Expected tools and arguments | Observable acceptance |
| --- | --- | --- |
| Compression: “Compress this original image-heavy PDF for email with balanced quality.” | Account check; `compress_pdf`, balanced; poll same handle. | Tool reports succeeded with a link; browser saves a smaller readable one-page PDF retaining expected content. |
| OCR variation: “Make each of these original scans searchable, English for the first and Spanish for the second.” | Account check; `make_pdf_searchable`, `eng` then `spa`, separate jobs; poll each. | Both downloads contain expected searchable text, original page dimensions and aligned text geometry. |
| Word: “Convert this original acceptance report to an editable Word document.” | Account check; `convert_pdf_to_word`; poll same handle. | Browser saves a valid DOCX with editable expected fixture text, not a PDF renamed as DOCX. |
| Merge: “Combine two-pages.pdf followed by text.pdf, preserving that order.” | Account check; `merge_pdf`, two descriptors in supplied order; poll same handle. | Three-page PDF; all pages match original text/rendered pixels and their requested order. |
| Split/extract: “Split the original two-page PDF into page 2 then page 1. Also extract only page 1 as a separate result.” | Account check; `split_pdf` ranges `["2", "1"]` and a separate requested `["1"]` operation; poll each. | First result is a two-entry ZIP in reversed range order; second is a one-page PDF. Both match the original rendered pages. |

The OCR variation and split variation exercise seven processing jobs overall.
Across these cases, all seven exposed tools are covered, including minimal
account identification and status polling. Preserve every original; successful
model prose alone does not establish tool completion, download or content quality.

## Three negative cases

| Natural prompt | Required behavior |
| --- | --- |
| “Permanently redact and password-protect this PDF, then sign it.” | Explain these capabilities are not exposed by this integration. No processing call claiming to perform them. |
| “Buy me a higher DeftPDF subscription and show my billing history.” | Explain the plugin has no purchase, upgrade or billing-history access. No invented purchase or unrelated tool call. |
| “Use only this local PDF path; recreate it from text if necessary so you can split it.” | Do not reconstruct or substitute the original. Stop without processing; explain the authenticated original-file web upload step. A minimal account check is permitted. |

## Recovery and boundaries

- Wrong account: reject another account's descriptor/handle without exposing it.
- Missing/expired/invalid PDF: return an actionable error; do not fake success.
- Pending or lost response: retain the existing handle; do not submit a new job.
- `SUBMISSION_UNKNOWN` with `can_poll: false`: stop and reconcile through support.
- Duplicate private request: recover the accepted task through durable replay;
  do not call it a new successful processing run.
- Blocked browser download: record the client failure. Do not disable browser
  protection or fetch a blocked signed URL through another transport and label
  that browser acceptance.
- Review every tool in both the official MCP Inspector and the intended Claude
  client before making the portal's test acknowledgement. SDK tests are separate.

## Evidence boundary

Prior private acceptance covered real browser original-byte uploads, all seven
hosted-Claude processing cases, actual browser downloads and output checks;
independent Claude Code plugin OAuth, setup, local-path refusal, split/polling and
a browser download were also verified. Those facts do not establish directory
approval, a successful directory installation, public account eligibility, or
Cowork support. Record new review runs against the actual submitted commit and
account in private operator evidence, using Passed/Failed/Blocked/Not run.
