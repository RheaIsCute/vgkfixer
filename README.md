# vgkfixer

Static report viewer for VGKFIXER, hosted on GitHub Pages at https://rheaiscute.github.io/vgkfixer/.

VGKFIXER's **COPY LINK** button produces links like `https://rheaiscute.github.io/vgkfixer/r/#1z.<data>`. The report is JSON, deflate-compressed and base64url-encoded, and it sits in the URL fragment. Browsers never send the fragment to the server, so GitHub never receives or stores any report. `r/app.js` decodes the report in the reader's browser.

The viewer treats link data as untrusted. It caps the decompressed size at 64 KB, validates every field, renders only with `textContent`, and runs under a strict Content-Security-Policy with no inline or third-party scripts.

## Payload (v1)

```json
{"v":1,"demo":false,"o":"complete","at":"<ISO time>","rt":"5.8s",
 "n":{"k":"Ethernet","s":"2.5 Gbps","a":"<adapter model>"},
 "st":[["<step title>","success|warning|error|running|pending","<detail>"]],
 "is":[["err|warn","<logged issue>"]]}
```

Prefix `#1z.` means deflate-raw compression; `#1u.` means uncompressed, the fallback for browsers without `CompressionStream`.
