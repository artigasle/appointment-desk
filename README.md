# Appointment Desk — GitHub Pages edition

A static appointment-letter generator. Enter organization and commander details, select a person and program appointments, and download one PDF per program. Runs without a build step, backend, API keys, third-party scripts, or installation.

## Start locally

Extract the ZIP and open `index.html` in a modern desktop browser. Keep `app.js`, `pdf.js`, and `style.css` beside it. The PDF generator works locally; no internet connection is needed after downloading the package. Browser-specific file restrictions may require serving the folder with `python3 -m http.server 8000` and opening http://localhost:8000.

## Publish on GitHub Pages

1. Create a GitHub repository for the generic application code. Do not include personnel records, generated appointment PDFs, or exported organization setup files.
2. Upload the contents of this folder (not the ZIP) to the repository root. `index.html` must be at the root.
3. Open the repository's **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**, then **main** and **/(root)**. Save.
5. Use the published URL shown in the Pages settings after deployment finishes.

No Actions workflow or package install is required. If your account restricts Pages or your organization requires a different publishing process, follow that account's controls. This repository publishes automatically from the root of `main` through GitHub Pages.

## Use

1. Fill organization, address, office symbols, commander name/title, and memo date.
2. Enter the appointee's rank, name, duty title, effective date, and point of contact.
3. Select one or more programs. Choose Primary or Alternate for each.
4. Expand **Edit program wording & qualification**. Replace starter references with verified publication/paragraph references; review the duties; enter a factually supported qualification statement.
5. Leave **DRAFT — FOR REVIEW** enabled for initial review. To remove it, complete the review acknowledgement. The acknowledgement is a user attestation, not formal compliance validation.
6. Generate letters. Download and review each PDF; review the text in the app as needed.
7. Download the `.eml` draft, open it in your email client, and attach the PDFs manually. Email-client support for opening `.eml` as an editable message varies; copy the text into a new message if needed. Nothing is sent automatically.
8. The commander should open each PDF in desktop Acrobat and apply their CAC certificate signature to the CommanderSignature field. Save and return the signed original without printing/converting it again.

The PDF is an appointment memorandum, not automatically an MFR. Set MEMORANDUM FOR to RECORD only when that format is appropriate for your approved process.

## Included programs

- Unit Safety Representative — starter wording only.
- Confined Space Program Team Representative — starter wording only; this does not appoint entry supervisors, attendants, entrants, or other confined-space roles.
- Add custom programs with your own validated title, authority, duties, qualifications, and template version.

All selected appointments receive separate letters, allowing independent replacement or revocation. Optional supersession text identifies only the specific letter you enter; it does not automatically revoke anything in a tracking system. Default appointments have no invented expiration or training deadlines.

## Reusable settings

**Export setup** saves organization details and reusable program wording to JSON. It excludes appointee details, qualification statements, effective/memo dates, selected roles, and selections. **Import setup** restores organization/template settings. Qualifying evidence must be entered for each appointee. Exported setups contain commander contact details and should remain in an authorized location, outside a public repository.

There is no automatic persistence or localStorage. Closing/reloading loses entered data. The page's Content Security Policy blocks fetch connections. GitHub still receives normal page requests; this does not make a public hosting environment approved for sensitive government data. Use only within your organization's authorized handling rules.

## Output and limitations

- US Letter, 1-inch body margins, 12-point embedded DejaVu Serif body text, multiline wrapping, page numbering, and a signature block kept with the final paragraph.
- A real unsigned AcroForm `/Sig` field is included in each PDF. This app neither accesses CAC keys nor signs or validates signatures. Acrobat/CAC compatibility and certificate trust must be verified on the intended workstation before operational use.
- Western European Latin-1 characters supported. Smart quotes and dashes normalize to ASCII. Unsupported scripts produce an explicit error instead of silently corrupting a person's name.
- No official seal, uploaded-letterhead support, automated routing, return collection, signature validation, records retention, or organizational authorization is implemented.
- No claim of AF-wide compliance. Verify current correspondence requirements, controlling program publications, local supplements, training/competence evidence, delegation authority, and letterhead before official use.
- Templates and layout require program-office approval. No requirement paragraphs have been invented. The starter publication names are research starting points, not verified current citations.
- The fixed PDF template can be adjusted in `pdf.js` after receiving an approved sample. Browser preview text is not a pixel-perfect PDF preview; use **Open PDF** to inspect the actual output.

## Files

- `index.html`: accessible form and user guidance.
- `style.css`: responsive layout.
- `app.js`: editable program templates, input validation, JSON setup handling, PDF links, and email draft.
- `pdf.js`: dependency-free PDF writer with embedded subset font and unsigned signature widget.
- `FONT-LICENSE.txt`: license for the embedded DejaVu Serif font.
- `tests/pdf.test.cjs`: Node 18+ PDF smoke tests; run `node tests/pdf.test.cjs`. Outputs go to `tests/output/` (ignored by Git).
- `.nojekyll`: serves as a plain static site.

## Verification performed

- JavaScript syntax checks.
- Browser form flow with fictional information, program selection, qualification entry, and successful generation of PDF and email download links.
- PDF structural validation using pypdf: a single unsigned `/Sig` field on the final page, linked through the AcroForm field tree and page annotation.
- One-page and seven-page outputs; long-word wrapping; accented text; explicit rejection of unsupported characters.
- Visual inspection of the generated sample PDF.

Not tested: actual CAC signing, certificate trust/revocation validation, government workstation browser policies. Test with a non-operational sample before use.

## Future Microsoft 365 edition

The organization and program model can be mapped to SharePoint lists. Routing, authenticated access, signed-original storage, signature validation, and return tracking belong in that separate deployment. The current package does not connect to Microsoft 365.
