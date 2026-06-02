# Overview repro

building-bioinformatics/\
├── \_quarto.yml\
├── index.qmd\
├── about.qmd\
├── blog.qmd\
├── notes/ \# raw notes, tracked in Git, not rendered\
├── drafts/ \# draft .qmd files, not published\
├── posts/ \# published posts\
├── assets/\
│ ├── images/\
│ └── css/\
└── .gitignore

# Workflow

## Stage 1 — raw capture

While learning or experimenting:

```         
notes/
```

Examples:

```         
notes/computing-infrastructure.md
notes/bioinformatician-profiles.md
notes/git-workflows.md
notes/github-vs-gitlab.md
```

## Stage 2 — draft article

Once an idea matures:

Move/refactor into:

```         
drafts/
```

Example:

```         
drafts/computing-infrastructure.qmd
```

Now:

-   reorganize

-   add sections

-   add diagrams/ figures

-   verify technical accuracy

-   improve flow

-   add references

## Stage 3 — finalize

Only polished content goes into:

```         
posts/
```

Example:

```         
posts/2026-05-19-research-network-architecture/
```

Containing:

```         
index.qmd
images/
```

## Stage 4 — publication

Render quarto documents into html (stored by default in ./docs)

```         
quarto render
```

Push to Github for publication with Github Pages

```         
# check status
git status

# may be pull updates
git pull

# push content
git push
```

(\*probably should set up GitHub actions to do Stage 4)
