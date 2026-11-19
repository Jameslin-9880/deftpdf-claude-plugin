---
name: setup
description: Connect a DeftPDF account and explain private PDF uploads in Claude Code.
disable-model-invocation: true
---

# Set up DeftPDF

1. Check whether DeftPDF MCP tools are connected. Claude Code can suppress this
   plugin's duplicate server when a manually configured connection already uses
   https://mcp.deftpdf.com/mcp. In that case reuse that exact-endpoint connection
   and verify its account in step 2; do not change unrelated connections. If authorization
   is needed, tell the user to open `/mcp`, select that DeftPDF connection
   (the plugin server or the matching existing manual connection),
   and complete the normal browser OAuth consent. Do not add a second MCP server,
   read browser cookies or credential databases, request passwords/API keys, or
   change other connections. Never print OAuth callbacks or tokens.
2. Call the selected DeftPDF connection's `get_deftpdf_account` tool and show the connected display
   name. If the user expected another account, stop before processing and use
   `/mcp` to reconnect this server. Do not expose internal account identifiers.
3. Explain that the current tools cannot upload a local file path, Claude chat
   attachment, or bytes read with `Read`. To process an original PDF, the user
   signs into https://deftpdf.com/mcp/input as the same account, selects the
   original PDF, uploads it privately, and copies its file descriptor into this
   conversation. This is an explicit web upload, not native attachment transfer.
4. Private upload access is currently limited to approved accounts. Installing
   this plugin does not grant access or change plan entitlements. If the page
   reports unavailable or forbidden, stop and explain that access is restricted;
   do not use a public/reconstructed substitute or change an account/feature gate.
5. Explain `/deftpdf:pdf`: compression, searchable English/Spanish OCR, editable
   Word conversion, ordered merging, and splitting/extraction. Files go to
   DeftPDF for processing; outputs are temporary signed downloads. See
   [privacy and limits](../../references/privacy-and-limits.md).

If the account call succeeds, state that the connection is ready. Do not claim
that upload, processing, or download has passed until each actually happens.
