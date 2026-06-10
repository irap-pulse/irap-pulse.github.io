# Security policy — IRAP Pulse

## Reporting a vulnerability

If you find a security issue — for example a way for a malicious file to execute code in the user's browser, or a way for the tool to leak data off the client — please report it privately rather than opening a public GitHub issue.

Contact: LinkedIn DM to <https://www.linkedin.com/in/gauravvikash/>

We will acknowledge within a few days, work on a fix, and credit you in the release notes unless you prefer to stay anonymous.

Please do not attach real SSP-As, CCMs or customer data to your report. Redact identifiers and wording, or reproduce the issue using the sample data.

---

## Security posture of the current release

**Malware scan.** The tool has been scanned via VirusTotal prior to each release. No threats detected.

**Static analysis.** The HTML source was scanned for common client-side risk patterns prior to release:

| Check | Result |
| --- | --- |
| `fetch()` calls | Limited to the three bundled ASD data files (relative paths) and the two CDN library loads on startup. No other outbound calls. |
| `XMLHttpRequest`, `WebSocket`, `sendBeacon`, `EventSource` | Zero occurrences |
| `eval()`, `new Function()`, string-form `setTimeout`/`setInterval` | Zero occurrences |
| `innerHTML` assignments | All occurrences reviewed. User-derived strings are wrapped in the `escapeHtml()` helper (escapes `& < > " '`). |
| External URLs | Limited to the two SRI-pinned CDN script tags, the pdf.js worker (SRI not applicable — browser limitation), and static outbound links to cyber.gov.au, cybernion.com.au and the author's LinkedIn profile. |

**Subresource Integrity.** Both JavaScript libraries are loaded with SRI hashes pinned to exact versions. The browser will refuse to execute either if the CDN serves a modified file.

**Bundled file integrity.** On every page load, the tool computes SHA-256 hashes of the three bundled ASD data files and compares them against expected values embedded in the HTML at release time. A mismatch is displayed visibly in the interface.

**No server component.** The tool is a single HTML file. There is no backend, no authentication surface, no database, and no session state stored outside the browser tab.

**Data handling.** Files uploaded by the user are parsed in-browser only and are not transmitted anywhere. Closing or reloading the tab discards all state.

---

## Responsible use

You are responsible for handling uploaded files in line with your organisation's data-classification, data-sovereignty and record-keeping obligations. The tool is client-side and does not transmit data, but the files remain on your device — ensure that device is authorised for the classification of material being processed.

Do not process SECRET or TOP SECRET material on a device that is not accredited for that classification.
