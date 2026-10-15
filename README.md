# Obsidian Vault

This repository contains my personal PKM (Personal Knowledge Management) system built in Obsidian. It follows a structured, domain-oriented approach designed to separate raw source inputs from evergreen knowledge, maintain a maximum directory depth of 3 levels, to avoid deep trees of folders hiding files and minimize friction during note-taking.

---
## 1. Vault Structure

```text
.
├── 01_Knowledge/                       # Evergreen Single Source of Truth
│   ├── Computer Science/               
│   ├── Software Engineering/           
│   ├── Cybersecurity/                  
│   ├── Mathematics/                    
│   ├── Languages/                      
│   └── Competitions/                   
├── 03_Sources/                         # Raw Inputs & Linear Captures
│   ├── Books/
│   ├── College/                        # Raw lecture notes & course materials
│   ├── Courses/
│   ├── Articles & Media/
│   └── Inbox.md                        # Quick-capture staging file
└── 04_Meta/                            # Vault Administration
    ├── Attachments/                    # Embedded images and media files
    └── Templates/                      # Obsidian note templates
````

This structure can grow as I learn more domains.

## 2. Core Structural Principles

### Maximum 3-Level Folder Depth

Directories never exceed 3 levels deep (`Category / Domain / Sub-Domain`). To prevent folder explosion and tedious navigation. To further categorize notes inside Level 3 folders, I use **prefixed file naming** (e.g., `DS - Segment Tree.md`, `Algo - Dijkstra.md`) to logically group related files alphabetically.

### Separation of Note Taking and Knowledge Declaration

For notes that I take for college classes, courses, or books, I keep them under `02_Sources`, and each source that I learn from and take notes from might contain duplicated information. This is fine and by design, as I will only extract knowledge that I deem is important to the `01_Knowledge` directory later on.

  
## 3. Note Lifecycle & Information Flow

Information moves through a 3-phase pipeline to prevent vault bloat and maintain a high standard of synthesized knowledge:

```
[ Raw Inputs ]               [ Temporary Staging ]         [ Evergreen Vault ]
Book / Lecture / Media  ──►  03_Sources/ or Inbox.md  ──►  02_Knowledge 
```

1. **Capture (Raw Sources):**
    - Lecture notes, book chapters, and structured courses are recorded sequentially in `03_Sources/` 
    - One-off YouTube videos, blog posts, or quick discoveries are dumped directly into `03_Sources/Inbox.md`.

2. **Distill (Knowledge Synthesis):**
    - Core concepts, algorithms, proofs, or theorems are extracted into atomic, single-topic notes inside `02_Knowledge/`.
    - A single Knowledge Note synthesizes understanding across all sources (books, lectures, papers) into one definitive reference file.

3. **Connect & Triage:**
    - Source notes link upward to their corresponding Knowledge Notes.
    - `Inbox.md` is periodically cleared once key takeaways are integrated into `02_Knowledge/`.

## 4. Note Standards & Conventions

### Heading Hierarchy
- **No Manual `#` (H1) Headings:** Obsidian's _Inline Title_ setting displays the file name as the document's `H1`. Notes begin directly with `##` (H2) section headings to preserve clean document outline hierarchy and screen-reader accessibility.
### Knowledge Note Template Structure

Each note in `02_Knowledge/` follows a standard template, which can be found in the `03_Meta/Templates/` folder.

### Unlinked Mentions & Aliases

Because atomic notes use prefixes (e.g., `DS - Segment Tree.md`), the `aliases` property in the YAML frontmatter is required:

```yaml
---
aliases:
  - Segment Tree
  - segment tree
---
```

This ensures that Obsidian's auto-complete, graph connections, and unlinked mention detectors recognize variations of the concept automatically.