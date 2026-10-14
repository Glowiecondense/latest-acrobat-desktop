# acrobat pro

People type this because they want to edit a PDF and something told them Acrobat is the tool that does it. That is the whole intent behind the query. The rest of this page is about Adobe Acrobat Pro: what it actually is, how the editions and names fit together, where the work happens, and which parts routinely go wrong.

![Acrobat performers lit up on stage](assets/cover.jpg)
*The word "acrobat" belonged to performers long before it belonged to a file format. Same spelling, unrelated things.*

## Why the query looks the way it does

The pack of searches around this subject is noisy in a specific way. `adobe acrobat pro`, `adobe acrobat professional`, `acrobat professional`, and `adobe acrobat professional dc` are the same product with different words attached. `adobe acrobat pro dc` and `adobe pdf pro dc` come from the years when "DC" was part of the name. `acro pro` is shorthand. `adobe pro` and `adobe professional` are truncated — people stop typing once the autocomplete shows something plausible. `adobe professional pro` and `adobe creator pro` are typos that happen to land near the same thing.

The intent behind all of them is close to identical: find the desktop application that opens a PDF, lets you change the text, and saves it back as a PDF. `adobe acrobat pro pdf editor` spells that out explicitly. So this page treats them as one subject.

## What Acrobat Pro is, and what Reader is not

Adobe Acrobat Pro is the paid desktop application for authoring and repairing PDFs. Acrobat Reader — now just "Acrobat Reader" — is the free viewer: it opens, prints, fills simple forms, and can add a basic signature, but it cannot change existing text, reorder pages by dragging, run OCR, or apply preflight profiles. If someone hands you a PDF and says "just fix the typo," Reader is the wrong window.

The PDF format itself is an ISO standard (ISO 32000), and Acrobat is one implementation of it, not the definition. That matters when a file behaves strangely: the problem is often the file, not the reader.

![Aviatika Acrobat A-900 at the Paris Air Show, 1993](assets/photo.jpg)
*The Aviatika Acrobat A-900, Paris Air Show, 1993. The name has been reused by aircraft makers too — worth knowing when a search result looks wrong.*

## The naming maze: Professional, DC, and plain Pro

The product has been renamed more often than most software:

- **Acrobat 6 Professional (2003)** introduced the split between Standard and Professional. Professional added preflight, form authoring, and print-production checks.
- **Acrobat 7, 8, 9, X, XI** continued that split through the 2000s and early 2010s.
- **Acrobat DC (2015)** — "Document Cloud" — moved to a continuous release track, which is why `adobe acrobat pro dc` is still such a common search.
- **Acrobat 2017 and Acrobat 2020** were the classic, perpetual-license tracks sold alongside the DC subscription.
- **Around 2023** Adobe dropped "DC" from the product name. Current builds are simply **Acrobat Pro** and **Acrobat Standard**, with a web version for lighter tasks.

So "Acrobat Pro DC" is not a different program from "Acrobat Pro." It is the same lineage with an older label. `adobe acrobat professional dc` and `adobe acrobat pro dc software` are just longer ways of writing the same thing. Standard sits below Pro: no preflight, no full redaction tooling, no Compare Files, no Action Wizard.

## Editing, OCR, and forms

Editing text in a PDF is not like editing a Word document, and Acrobat does not pretend otherwise. A PDF stores positioned glyphs, not paragraphs. When you click into a line, Acrobat reconstructs an approximate text run from those glyphs. If the original font is not installed on your machine, Acrobat substitutes a similar one, and the line spacing can shift. Short edits are fine. Rewriting a whole paragraph is usually better done by going back to the source document.

Scanned pages are pictures of text. **Tools > Scan & OCR > Recognize Text** runs OCR and adds an invisible text layer, which makes the page searchable and selectable. It does not make the page editable in the ordinary sense — the visible content is still an image. Run OCR first, then edit, or the editing tools will have nothing to work with.

Forms come in two kinds. **AcroForm** fields are the standard, portable kind that any viewer can fill. **XFA** forms, built with the old LiveCycle Designer, are a different animal: they render correctly in Acrobat and often poorly or not at all elsewhere. If a form looks blank in a browser but fine in Acrobat, it is probably XFA. Flattening the form — printing the filled values into the page — is the usual fix before sending it onward.

## Redaction, signatures, and archiving

Three features generate the most confusion.

**Redaction is not a black rectangle.** Drawing a filled box over a name leaves the text underneath, fully selectable and copyable. The correct path is **Redact > mark the content > Apply**. Only Apply removes the underlying characters. A redacted file that still contains the text is a genuine disclosure risk, and it happens constantly.

**Signatures are two different things.** A simple electronic signature — typed or drawn — is a visual mark with a certificate attached. A certificate-based digital signature, added with a signing credential, detects any later modification and shows a validity status in the signature panel. Acrobat Pro can create both; Reader can only do the simple kind.

**PDF/A is for archiving.** It restricts fonts, color, encryption, and embedded content so the file renders identically decades later. Acrobat's Preflight panel ships with PDF/A conversion profiles, and validating the result against a checker such as veraPDF is the honest way to confirm compliance rather than trusting the conversion dialog.

## Automating repetitive work

Two built-in tools save real time on batches.

The **Action Wizard** records a sequence — optimize, add header, run OCR, save with a naming pattern — and replays it across a folder of files. For anything you do more than twice a month, build an action.

The **JavaScript console** (enable it in Preferences, then open it from the Tools menu) gives you the document object model. This snippet stamps a dated footer on every page and locks the field so it cannot be edited afterward:

```js
// Acrobat JavaScript console: dated footer on every page, then lock it
for (var i = 0; i < this.numPages; i++) {
 var box = this.getPageBox("Crop", i);
 var f = this.addField("stamp" + i, "text", i,
 [box[0] + 36, box[1] + 24, box[0] + 300, box[1] + 46]);
 f.value = "Reviewed " + util.printd("yyyy-mm-dd", new Date());
 f.textSize = 8;
 f.readonly = true;
}
```

Acrobat's JavaScript is not browser JavaScript. There is no DOM, no `console.log`, and the API is documented separately. `this` is the open document; `util` and `app` are globals.

## Gotchas worth knowing before you start

- **File size.** A 40 MB scan is usually oversized images. **Save as Other > Optimized PDF** with downsampling to 150–200 dpi cuts it dramatically with no visible loss on screen.
- **Compare Files** (Tools > Compare Files) diffs two revisions and highlights changed text, which is far faster than reading both.
- **Accessibility.** **Autotag Document** infers a reading order from layout. It is a starting point; headings and table structure almost always need manual correction in the Tags panel.
- **Encryption and permissions** are set at save time and are easy to forget. A file that opens without a password on your machine may prompt on someone else's.
- **Version drift.** Acrobat's continuous track updates silently. If a script or action stops working, check whether the build changed before rewriting anything.

## Where it fits

Acrobat Pro is the heavy desktop option: full editing, OCR, redaction, preflight, form authoring, and batch automation in one application. Lighter needs — reading, commenting, signing, filling a standard form — are covered by Reader and by browser-based viewers, and there is no reason to reach for Pro to do them. Knowing which of the two you actually need is most of the answer to the query you typed.

---
Photos: maggie jones. · CC PDM pdm; Harry Clampers · CC BY by