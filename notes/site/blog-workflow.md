# Building Bioinformatics — Blog Workflow

Personal notes on how I organise, write, and publish posts for *Building Bioinformatics*.

## Repository Structure

```text id="a5y95e"
building-bioinformatics/
├── _quarto.yml
├── index.qmd
├── about.qmd
├── blog.qmd
│
├── notes/                    # ideas, references, experiments, rough notes
│
├── posts/
│   └── YYYY/
│       └── MM/
│           └── post-name/
│               ├── index.qmd
│               └── images/   # optional, post-specific images
│
├── assets/
│   ├── images/               # shared site images
│   └── css/
│       └── styles.css
│
├── docs/                     # rendered website (GitHub Pages)
├── README.md
└── .gitignore
```

Posts are organised by year and month. This makes it easy to see approximately when I worked on or published an article and prevents the `posts/` directory from becoming one long list of folders.

The exact publication date is stored in the post's Quarto metadata.

---

## 1. Notes

Most posts start life as notes.

Initial ideas, references, diagrams, code snippets, experiments, questions, and rough thoughts go into:

```text id="q7w1di"
notes/
```

These are working documents. They do not need to be polished, complete, or written for an audience.

The `notes/` directory is:

* tracked in Git;
* excluded from the rendered website;
* allowed to contain incomplete or exploratory material;
* retained even when a note later develops into a post.

Notes can be organised into subdirectories when useful, for example:

```text id="l05dhp"
notes/
├── git/
├── software-engineering/
├── infrastructure/
├── reproducibility/
├── fair-data/
└── ai/
```

There is no need to force every note into a category. The structure can develop naturally as the collection grows.

---

## 2. From Note to Post

When a topic starts becoming substantial enough for an article, create a new post rather than moving the original note.

The post goes under:

```text id="ybl4wa"
posts/YYYY/MM/post-name/
```

For example:

```text id="kyz5ta"
posts/
└── 2026/
    └── 09/
        └── understanding-git-branches/
            ├── index.qmd
            └── images/
```

The original material remains in `notes/`. It can continue to serve as a record of the learning process, references, experiments, or ideas that did not make it into the final article.

The post is the version written for readers.

---

## 3. Draft Posts

A new article starts as a Quarto draft.

A typical `index.qmd` begins with:

```yaml id="0krrl4"
---
title: "Understanding Git Branches"
description: "What Git branches actually are and how to work with them."
date: 2026-09-22
author: "Angelika Merkel"
categories:
  - Git
  - Software Engineering
draft: true
toc: true
---
```

While writing, the post stays under `posts/`. There is no separate `drafts/` directory.

The important distinction is:

```text id="pimcif"
notes/   = thinking, learning, experiments, source material

posts/   = articles written for the blog

draft: true = article still being developed
```

A draft is therefore a **state of a post**, not a separate type of document.

---

## 4. Images and Other Files

Files that belong specifically to one article should stay with that article:

```text id="p2j2m2"
posts/2026/09/post-name/
├── index.qmd
├── images/
│   ├── workflow.png
│   └── architecture.svg
└── ...
```

Images or resources used across the website belong under:

```text id="zhzz9g"
assets/
```

As a general rule:

```text id="y6eexw"
used by one post    → keep with the post
used across site    → assets/
```

This should make individual posts relatively self-contained and easier to maintain.

---

## 5. Writing and Previewing

During writing, preview the site locally:

```bash id="av8h0b"
quarto preview
```

This starts a local preview and automatically updates it as files change.

For longer posts, use:

```yaml id="cwywmx"
toc: true
```

Shorter posts do not necessarily need a table of contents.

Before publishing, check:

* title and description;
* publication date;
* categories;
* headings and structure;
* code blocks;
* figures and image paths;
* links;
* spelling and grammar;
* appearance on desktop and mobile;
* how the post appears in the blog listing.

---

## 6. Publishing a Post

When the article is ready, remove:

```yaml id="i5lg2a"
draft: true
```

Then render the complete website:

```bash id="1avcxv"
quarto render
```

Check the rendered site locally, particularly:

```text id="ht62kj"
docs/
```

Then check the Git changes:

```bash id="36c14r"
git status
```

Commit the source and rendered website:

```bash id="x06vzr"
git add .
git commit -m "Publish <post name>"
git push
```

GitHub Pages serves the website from the `docs/` directory.

---

## 7. Git Strategy

The normal writing workflow does not require a Git branch.

Notes, drafts, and normal article revisions can be committed directly to `main`.

Use a separate branch when experimenting with changes that affect the website itself or could temporarily break it, for example:

```text id="t6n7ao"
redesign-homepage
change-post-layout
add-search
new-navigation
update-site-styling
```

The distinction is:

```text id="nyvr32"
CONTENT STATE
    ↓
Quarto draft mechanism

WEBSITE / CODE DEVELOPMENT
    ↓
Git branches
```

Do not create branches simply because an article is unfinished. Quarto's draft mechanism already represents that state.

---

## 8. Overall Workflow

```text id="1g3n6b"
idea / question / something I want to understand
                    ↓
                  notes/
                    ↓
       read / test / experiment / learn
                    ↓
          enough material for a post?
                    ↓
                   yes
                    ↓
       posts/YYYY/MM/post-name/
                    ↓
               draft: true
                    ↓
          write / test / revise
                    ↓
          check local preview
                    ↓
          remove draft status
                    ↓
              quarto render
                    ↓
             check git status
                    ↓
              commit + push
                    ↓
                 publish
```

The main principle is to keep the workflow simple.

`notes/` is where I can think freely and collect material. `posts/` contains material that is being developed for readers. Quarto handles whether a post is a draft or published, and Git records how everything changes over time.
