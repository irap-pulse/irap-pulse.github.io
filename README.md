# IRAP Pulse

**By [Cybernion](https://cybernion.com.au/) · Built by [Gaurav Vikash](https://www.linkedin.com/in/gauravvikash/)**

A free, single-file, browser-based tool for Australian government and enterprise security teams managing ISM compliance. Everything runs in your browser — no backend, no account, no data leaves your machine.

---

## What it does

IRAP Pulse has two tools in one:

### Tab 1 — Create SSP-A

Generates a pre-populated System Security Plan Annex (SSP-A) from a blank ASD template. Select your system classification and tick the ISM Guidelines that apply to your system. The tool writes a consistent Not Applicable status and justification into every excluded control, leaving all other controls as Not Assessed for you and your assessor to work through.

This eliminates the most tedious part of starting an SSP-A — manually marking hundreds of controls NA before the real assessment work begins.

### Tab 2 — Update SSP-A or CCM

Computes the quarterly delta between your current SSP-A (or a prior-quarter CCM) and the latest ASD Cloud Controls Matrix. For each changed control the tool pre-fills scoping decisions it can determine mechanically from your own baseline, surfaces cross-validation inconsistencies, and produces three reviewer-ready exports.

**Outputs:**

| Export | What it contains |
| --- | --- |
| Change Register (.xlsx) | Summary, Controls, Principles, Methodology, E8 Snapshot tabs. Full context and editable triage fields for every changed control. |
| Updated Baseline (.xlsx) | Your SSP-A rewritten against the current quarter — new rows inserted, rescinded rows removed, modified rows flagged. |
| Stakeholder note | Plain-English draft for leadership or technical teams, editable before copying. |

---

## Who this is for

- Australian government agencies and cloud service providers running quarterly ISM impact assessments
- IRAP assessors and implementors preparing or reviewing an SSP-A
- Security and compliance teams maintaining a live SSP-A against the ISM

---

## How to use

### Tab 1 — Create SSP-A

1. Open `index.html` in a browser
2. Enter your organisation name
3. Select **Use ASD's current SSP-A Template** (bundled) or upload your own blank ASD template
4. Select your system classification
5. Review the Guidelines list — pre-ticked Guidelines apply to most systems. Untick any that genuinely do not apply and provide a brief justification
6. Click **Download updated SSP-A (.xlsx)**

### Tab 2 — Update SSP-A or CCM

1. Enter organisation name, product name, classification and a short product overview
2. Upload your current SSP-A or CCM baseline (.xlsx)
3. The current-quarter CCM and ISM Changes PDF load automatically
4. Click **Update**
5. Review the dashboard — edit In Scope, Triage, Recommended Action and Owner/Notes inline
6. Export before closing the tab — the tool does not persist session state

---

## Privacy and security

- **No data leaves your machine.** All processing is in-browser. Nothing is transmitted to any server.
- **Two JavaScript libraries** are loaded at startup from public CDNs: [xlsx-js-style v1.2.0](https://github.com/gitbrent/xlsx-js-style) and [pdf.js v3.11.174](https://github.com/mozilla/pdf.js). Both are pinned to exact versions with Subresource Integrity (SRI) hashes — the browser refuses to run either if the CDN serves a modified file.
- **Bundled file integrity.** On load, the tool computes SHA-256 hashes of the bundled CCM, Changes PDF and SSP-A template and compares them against expected values embedded in the HTML at release time. A Verified result confirms the files are byte-for-byte identical to those tested by the author.
- Both libraries were scanned against public vulnerability databases prior to release. No known vulnerabilities were identified at the pinned versions.
- The full source is in `index.html`. Inspect it in any text editor or browser developer tools.

See [SECURITY.md](SECURITY.md) for the full security policy and how to report a vulnerability.

---

## Bundled files

Each quarterly release ships three ASD artefacts alongside `index.html`:

| File | Contents |
| --- | --- |
| `ccm-current.xlsx` | Current-quarter ASD Cloud Controls Matrix |
| `ism-changes-current.pdf` | Current-quarter ISM Changes PDF |
| `sspa-template-current.xlsx` | Current blank ASD SSP-A template |

Replace all three files and update the `BUNDLED_FILE_HASHES` constant in `index.html` at the start of each quarter. The SHA-256 values to use are printed by running `sha256sum ccm-current.xlsx ism-changes-current.pdf sspa-template-current.xlsx`.

---

## Known limitations

- **Sensitivity labels.** SSP-As protected with Microsoft Purview / AIP labels cannot be parsed — the browser sees ciphertext. Remove the label, save a clean copy, upload that, then re-apply the label to your original.
- **Password-protected workbooks.** Not supported. Convert to a plain `.xlsx` before uploading.
- **Column layout.** The tool expects ASD's standard CCM and SSP-A column headers. If ASD restructures the CCM in a future quarter, spot-check a few rows and update the column-detection regexes in the source if needed.
- **Rescission and re-issue.** When ASD retires one identifier and reintroduces the same requirement under a new one, the tool flags the old as Rescinded and the new as New. Likely pairs are hinted at in the dashboard but not auto-linked.
- **Freeze panes.** The underlying library does not write frozen rows. Apply manually in Excel after download (View → Freeze Top Row).

---

## Disclaimer

This tool is provided free of charge on an "as is" basis. The output is a decision-support aid — not professional, legal, compliance, assurance or IRAP advice. You remain solely responsible for reviewing every output, confirming every Not Applicable decision, and ensuring final artefacts meet your organisation's assurance and accreditation obligations.

See [LICENSE](LICENSE) for the full terms.

---

## Not affiliated with ASD or the Australian Government

"ISM", "Cloud Controls Matrix", "Essential Eight", "IRAP" and related terms refer to work published by the Australian Signals Directorate / ACSC. IRAP Pulse is an independent utility and is **not endorsed by, affiliated with, or sponsored by** ASD, ACSC or the Australian Government.
