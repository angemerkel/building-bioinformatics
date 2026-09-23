# Building Bioinformatics

Practical notes on bioinformatics, software, reproducibility, workflows, and research infrastructure.

Bioinformatics has changed enormously over the last twenty years. What started as a discipline focused largely on analysing biological data has expanded to include complex workflows, software engineering practices, research computing, data management, reproducibility, and the infrastructure needed to support modern computational research.

Like many bioinformaticians of my generation — those who grew up with Perl scripts, shell pipelines, and mysterious cluster queues — I learned most of these things while trying to solve real research problems. Formal training in software engineering, reproducibility, infrastructure, or data management was rare, and much of it we had to figure out as we went along. The current generation of bioinformaticians is certainly better prepared, but many of the practical aspects of building sustainable and reproducible computational research environments are still learned through experience.

*Building Bioinformatics* is my attempt to put into writing things I have observed, experienced, or been thinking about over the years, as well as things I am learning, revisiting, or simply curious about. Some posts go deeper into topics I previously encountered while solving a particular problem; others explore how the different pieces of modern bioinformatics fit together.

Some posts are tutorials, some are reflections, and some are simply things I wish somebody had explained to me earlier in my career.

**Website:** https://angemerkel.github.io/building-bioinformatics/

## Repository Structure

```text
building-bioinformatics/
├── _quarto.yml
├── index.qmd
├── about.qmd
├── blog.qmd
├── notes/                    # ideas, references, experiments, rough notes
├── posts/
│   └── YYYY/
│       └── MM/
│           └── post-name/
│               ├── index.qmd
│               └── images/   # optional, post-specific images
├── assets/
│   ├── images/
│   └── css/
├── docs/                     # rendered website (GitHub Pages)
└── README.md
```

## Writing Workflow

My posts start life as notes. Initial ideas, references, diagrams, code snippets, experiments, and rough thoughts go into `notes/`, which is tracked in Git but excluded from the rendered website.

When a topic develops into an article, I create a post under `posts/YYYY/MM/post-name/`. Posts that are still being developed use `draft: true` in their Quarto metadata and are published by removing the draft status once they are ready.

The original notes remain in `notes/` as working material and source material for future posts.

## Local Development

I usually work on the site in RStudio.

Preview the site locally:

```bash
quarto preview
```

Render the full site:

```bash
quarto render
```

The rendered website is written to `docs/` and published through GitHub Pages.

## About the Author

I'm Angelika Merkel, a biologist turned bioinformatician who somehow ended up spending as much time thinking about software, infrastructure, and data management as biology itself. Working in large research collaborations and later leading a bioinformatics facility certainly helped along the way.

After more than two decades working in genomics, epigenomics, and biomedical research, I'm still learning, still catching up with new technologies, and still fascinated by the challenge of connecting biology, data, software, and infrastructure in ways that make research work better.
