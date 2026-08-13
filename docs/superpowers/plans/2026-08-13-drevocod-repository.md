# DREVOCOD Repository Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and publish the verified first version of the private `Romario499/DREVOCOD` brand repository.

**Architecture:** Keep approved verbal brand materials in focused Markdown files under `brand/`, reserve `website/` and `assets/` for future supplied materials, and store decisions under `docs/`. Build and validate locally first, then create the private GitHub repository and publish the exact reviewed state to `main`.

**Tech Stack:** Markdown, Git, GitHub, PowerShell validation; no runtime dependencies.

**Spec:** `docs/superpowers/specs/2026-08-13-drevocod-repository-design.md`

## Global Constraints

- Repository owner is `Romario499`; repository name is exactly `DREVOCOD`.
- GitHub visibility must be private and the default branch must be `main`.
- The recovered presentation text is the primary source for verbal positioning.
- Brand language must not be represented as proof of operational capability.
- Do not invent products, materials, production capacity, technologies, certifications, team history, geography, prices, customers, timing, warranties, contacts, or launch status.
- Do not edit, rename, move, delete, or automatically copy anything under the local `sources/` directory.
- Do not add dependencies.
- GitHub Project boards are out of scope.

---

### Task 1: Create the repository documentation scaffold

**Files:**
- Create: `.gitignore`
- Create: `README.md`
- Create: `website/README.md`
- Create: `assets/README.md`
- Create: `assets/logo/.gitkeep`
- Create: `assets/images/.gitkeep`
- Create: `assets/fonts-reference/.gitkeep`
- Create: `docs/README.md`

**Interfaces:**
- Consumes: the approved design specification and global constraints.
- Produces: the stable directory map referenced by all brand documents.

- [ ] **Step 1: Create `.gitignore`**

Include operating-system files, editor metadata, logs, dependency directories, build output, local environment files, and secrets while keeping tracked Markdown and `.gitkeep` files visible. Required patterns:

```gitignore
.DS_Store
Thumbs.db
Desktop.ini
.idea/
.vscode/
*.log
node_modules/
dist/
build/
.env
.env.*
!.env.example
*.local
```

- [ ] **Step 2: Create the root README**

Use these sections: `DREVOCOD`, `Код природы. Язык пространства.`, `О проекте`, `Что уже зафиксировано`, `Структура репозитория`, `Правила работы с фактами`, and `Текущий статус`. State that the repository currently stores the brand foundation and preparation materials; do not state that a catalogue, production facility, sales operation, or live website exists.

- [ ] **Step 3: Create scope README files and asset placeholders**

`website/README.md` must reserve the directory for future website source. `assets/README.md` must explain the `logo/`, `images/`, and `fonts-reference/` subdirectories and require source/licence information for added assets. `docs/README.md` must reserve the directory for decisions, research, and specifications. Add `.gitkeep` to all three empty asset subdirectories.

- [ ] **Step 4: Verify the scaffold**

Run:

```powershell
$required = @('.gitignore','README.md','website/README.md','assets/README.md','assets/logo/.gitkeep','assets/images/.gitkeep','assets/fonts-reference/.gitkeep','docs/README.md')
$missing = $required | Where-Object { -not (Test-Path $_) }
if ($missing) { throw "Missing paths: $($missing -join ', ')" }
```

Expected: command completes without output or exception.

- [ ] **Step 5: Review the task scope**

Run `git status --short` if Git is initialized; otherwise list the created paths. Confirm nothing under `sources/` changed.

### Task 2: Preserve the approved presentation text

**Files:**
- Create: `brand/presentation-text.md`

**Interfaces:**
- Consumes: the complete presentation text recovered from conversation `6a7da98e-4364-83eb-8e6f-bd8b36113ed1`.
- Produces: the primary verbal source used by `positioning.md`, `tone-of-voice.md`, and `brand-system.md`.

- [ ] **Step 1: Create the presentation document**

Copy the recovered text from `# DREVOCOD` through the closing formulation `Природа уже создала код. Мы превращаем его в форму.` Remove only the conversation writing-block wrapper. Preserve all substantive headings, sentences, emphasis, and sequence.

- [ ] **Step 2: Verify source anchors**

Run:

```powershell
$text = Get-Content -Raw -Encoding UTF8 'brand/presentation-text.md'
$anchors = @('Код природы. Язык пространства.','DREVO + CODE','Материал как главный герой','Современное ремесло','Эстетика DREVOCOD','Принципы DREVOCOD','Природа уже создала код.')
$missing = $anchors | Where-Object { $text -notmatch [regex]::Escape($_) }
if ($missing) { throw "Missing anchors: $($missing -join ', ')" }
```

Expected: command completes without output or exception.

- [ ] **Step 3: Check the ending and encoding**

Read the first and final 20 lines with UTF-8 encoding. Confirm the title, slogan, final formulation, and Cyrillic characters are intact.

### Task 3: Create the derived verbal brand documents

**Files:**
- Create: `brand/positioning.md`
- Create: `brand/tone-of-voice.md`
- Create: `brand/brand-system.md`

**Interfaces:**
- Consumes: `brand/presentation-text.md` and the global unsupported-claim boundaries.
- Produces: concise positioning, writing guidance, and versioned verbal-system rules for future brand and website work.

- [ ] **Step 1: Create `positioning.md`**

Include: document status, positioning core, DREVO + CODE meaning, role of material, approach, audience language present in the approved text, principles, and a strict `Границы подтверждённых фактов` section. Qualify the document as a brand platform, not evidence of current products or services.

- [ ] **Step 2: Create `tone-of-voice.md`**

Define six qualities: calm, precise, tactile, contemporary, restrained, and human. Add sentence-pattern guidance, preferred vocabulary taken from the presentation text, prohibited hype and unsupported promises, and paired `Допустимо` / `Не допускается` examples.

- [ ] **Step 3: Create `brand-system.md`**

Set version `0.1` and include the approved name, main slogan, closing formulation, semantic formula, verbal pillars, vocabulary, content hierarchy, and governance rules. Mark logo, palette, typography, photography, graphics, layout, and motion as unconfirmed visual-system decisions without proposing values.

- [ ] **Step 4: Run the unsupported-claim review**

Search all initial Markdown files for concrete claims involving prices, named products, workshop/factory ownership, capacity, delivery, warranty, certification, years of experience, clients, geography, contacts, or order acceptance. Inspect every match in context; allow a term only when it appears inside an explicit prohibition or boundary statement.

- [ ] **Step 5: Review cross-document consistency**

Confirm that the slogan, closing formulation, DREVO + CODE meanings, and principles do not conflict across the four brand files.

### Task 4: Initialize and validate the local Git repository

**Files:**
- Modify: local `.git/` metadata only through Git commands.
- Review: every intended project file except read-only `sources/` and local `AGENTS.md` context.

**Interfaces:**
- Consumes: the complete verified local repository contents from Tasks 1-3.
- Produces: a clean initial commit on local branch `main`, ready for publication.

- [ ] **Step 1: Initialize Git on `main`**

Run:

```powershell
git init -b main
```

Expected: a new local repository with current branch `main`.

- [ ] **Step 2: Inspect the exact untracked scope**

Run:

```powershell
git status --short
git status --short --ignored
```

Confirm no secrets or unintended files are staged. Keep `AGENTS.md` and `sources/` outside the DREVOCOD publication scope because they are local project context.

- [ ] **Step 3: Stage only intended paths**

Run:

```powershell
git add .gitignore README.md brand website assets docs
git diff --cached --stat
git diff --cached --check
```

Expected: only the DREVOCOD scaffold, brand documents, specification, and plan are staged; whitespace check exits successfully.

- [ ] **Step 4: Commit the reviewed initial state**

Run:

```powershell
git commit -m "docs: establish DREVOCOD brand foundation"
```

Expected: one root commit on `main`.

- [ ] **Step 5: Verify local Git state**

Run:

```powershell
git status --short --branch
git log --oneline -1
```

Expected: branch `main`, no tracked-file changes, and the initial commit visible.

### Task 5: Create and publish the private GitHub repository

**Files:**
- Modify: GitHub repository `Romario499/DREVOCOD`.
- Modify: local Git remote configuration.

**Interfaces:**
- Consumes: the reviewed local `main` commit from Task 4 and authenticated GitHub account `Romario499`.
- Produces: private remote repository `Romario499/DREVOCOD` with the verified initial commit on `main`.

- [ ] **Step 1: Recheck repository non-existence**

Use the connected GitHub account to search for the exact repository name and inspect the owner repository list. Stop if `Romario499/DREVOCOD` now exists and compare its contents before any write.

- [ ] **Step 2: Obtain action-time confirmation**

State the exact external change: create private repository `Romario499/DREVOCOD` and upload the reviewed initial commit. Do not submit the creation form until the user confirms.

- [ ] **Step 3: Create the repository**

In the authenticated GitHub interface, set owner `Romario499`, repository name `DREVOCOD`, and visibility `Private`. Do not add a generated README, `.gitignore`, licence, template, or GitHub Project because the local history already contains the required files.

- [ ] **Step 4: Connect and publish**

Use the remote URL returned by GitHub, add it as `origin`, and push local `main`. If the environment lacks authenticated Git push support, use a supported repository-content publishing workflow without exposing or requesting stored credentials.

- [ ] **Step 5: Verify remote metadata and contents**

Read the GitHub repository metadata and confirm: full name `Romario499/DREVOCOD`, visibility `private`, default branch `main`, and the expected root paths `README.md`, `brand/`, `website/`, `assets/`, `docs/`, `.gitignore`.

- [ ] **Step 6: Report completion**

Report the repository link, initial commit identifier, changed files, commands/checks run, validation results, and remaining content risks. Do not claim completion if remote visibility or content cannot be verified.
