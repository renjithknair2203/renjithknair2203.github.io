# Security Lab Notebook

A static (no build step, no Jekyll) portfolio site for showcasing hands-on cyber
security lab work. Each lab is written up as an "incident ticket" — ID, category,
tools, narrative, screenshots — which fits a SOC/IR job search better than a
generic project list.

Currently populated with 16 LetsDefend SOC-simulator investigations, converted
from the original Word docs: phishing/malware triage, web-attack detection
(SQLi, XSS, command injection, IDOR, LFI), and CVE exploitation cases (PAN-OS,
Checkpoint, SharePoint, Windows OLE). All screenshots were pulled from the
original documents and are already in `assets/img/`.

## 1. Put it on GitHub Pages

**Option A — personal site (recommended, gives you `yourname.github.io`)**
1. On GitHub, create a new repository named exactly `YOUR-USERNAME.github.io`
   (replace with your actual GitHub username).
2. Upload every file in this folder to that repo, keeping the folder structure
   (`index.html` at the root, `labs/`, `assets/` alongside it).
3. GitHub Pages is enabled automatically for this repo name. Your site will be
   live at `https://YOUR-USERNAME.github.io/` within a minute or two.

**Option B — project site (if you already use `yourname.github.io` for something else)**
1. Create a repo with any name, e.g. `security-lab-notebook`.
2. Upload the files the same way.
3. Go to **Settings → Pages**, set source to the `main` branch, root folder, and save.
4. Your site will be live at `https://YOUR-USERNAME.github.io/security-lab-notebook/`.

Easiest way to upload without using git on the command line: on the repo's GitHub
page, click **Add file → Upload files**, then drag the whole folder contents in.

## 2. Update your details

In `index.html`:
- Replace `YOUR-LINKEDIN`, `you@example.com`, `YOUR-GITHUB-USERNAME` in the hero
  section and footer with your real links.
- Add your CV as `assets/files/CV.pdf` (export your Word CV to PDF and drop it in
  that folder) — the "Download CV" button already points there.
- Edit the certifications grid if anything changes.

## 3. Turn a Word doc lab write-up into a page

Each lab has two parts:

**A. The case file card** on `index.html` (inside `<section id="labs">`) — a short
teaser that links to the full page. Copy an existing `<a class="case">` block,
give it a new `href="labs/lab-04.html"`, a `data-cat` (`network`, `siem`,
`forensics`, or `incident`), and a one-line summary of the lab.

**B. The full write-up page** in `labs/`. Copy `labs/lab-01.html` (it has
in-file comments explaining every section) to `labs/lab-04.html` and:

1. Update the `<title>`, ticket metadata, `<h1>`, and summary at the top.
2. Open your Word doc side by side. Most lab write-ups are already structured
   as Objective → Steps → Screenshots → Result — map each Word heading to an
   `<h2>` in the HTML and paste the paragraph text into `<p>` tags.
3. For screenshots: in Word, right-click an image → **Save as Picture** (or
   **File → Export → Change File Type** for the whole doc), save it into
   `assets/img/`, then reference it:
   ```html
   <figure>
     <img src="../assets/img/lab-04-firewall-rule.png" alt="Describe what's in the screenshot">
     <figcaption>Fig. 1 — one line on what this shows.</figcaption>
   </figure>
   ```
4. If a section quotes a command, query, or config, put it in a `<pre><code>`
   block so it renders in monospace like a terminal.
5. Delete the guidance comment near the top once you've replaced the content.

**Shortcut if you're short on time:** instead of retyping the whole write-up,
export the Word doc straight to PDF, drop it in `assets/files/`, and add a
"Full write-up (PDF)" link at the top of the lab's summary. You still get the
polished ticket-style landing page, and the PDF carries all your detail without
any reformatting work. You can always flesh the HTML version out later.

## 4. Add or remove labs

- To add one: duplicate a case card + a lab page as above, bump the ticket
  number, and update the "N logged" count in `index.html`.
- To remove the placeholder labs once you have real ones: delete the
  corresponding `<a class="case">` block and the `labs/lab-0X.html` file.

## File structure

```
index.html                homepage — profile, cert list, lab index
labs/lab-01.html          full write-up template (annotated — start here)
labs/lab-02.html          second placeholder lab
labs/lab-03.html          third placeholder lab
assets/css/style.css      all styling — one file, no build step
assets/img/               screenshots go here
assets/files/              CV.pdf and any PDF write-ups go here
```

No dependencies, no npm, no Jekyll — just static files GitHub Pages serves
directly.
