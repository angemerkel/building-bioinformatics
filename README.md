# Building Bioinformatics

Practical notes on bioinformatics, software engineering, reproducibility, research computing, and the infrastructure behind modern data-driven biology.

Bioinformatics has changed enormously over the last twenty years. What started as a discipline focused largely on analysing biological data now depends on complex workflows, software engineering, HPC and cloud infrastructure, FAIR data practices, machine learning, and increasingly AI.

Like many bioinformaticians of my generation—those who grew up with Perl scripts, shell pipelines, and mysterious cluster queues—I learned most of these skills while trying to solve real research problems. Formal training in software engineering, reproducibility, infrastructure, or data management was rare, and much of it we had to figure out as we went along.

Today's bioinformatics is no longer only about analysing data. It is about building workflows, software, infrastructure, and data systems that make research possible. While the current generation of bioinformaticians is undoubtedly better prepared, many of the practical aspects of creating sustainable and reproducible computational research environments are still learned through experience.

This blog is where I collect notes, lessons learned, ideas, and practical solutions from years of working at the intersection of biology, data, and software. Some posts are tutorials, some are opinion pieces, and some are simply things I wish somebody had explained to me earlier in my career.

**Website:** <https://angemerkel.github.io/building-bioinformatics/>

## Repository Structure

``` text
building-bioinformatics/
├── _quarto.yml
├── index.qmd
├── about.qmd
├── blog.qmd
├── notes/          # ideas, references, rough notes
├── posts/          # drafts and finished articles
├── assets/
│   ├── images/
│   └── css/
├── docs/           # rendered website (GitHub Pages)
└── .gitignore
```

## Writing Workflow

Most of the posts start life as notes. Initial ideas, references, diagrams, and rough thoughts go into the `notes/` folder. When a topic starts taking shape, it gets moved into `drafts/`. Once a post is ready for publication, I move it to `posts/` and it becomes part of the website.

The idea is to keep the thinking, drafting, and publishing stages separate while tracking everything in Git.

## Local Development

Preview the site locally (in practice, do this using POSIT formerly Rstudio):

``` bash
quarto preview
```

Render the full site:

``` bash
quarto render
```

## Publishing

The site is built with Quarto and published through GitHub Pages from the `docs/` directory.

After rendering:

``` bash
git add .
git commit -m "Add new post"
git push
```

## About the Author

I'm Angelika Merkel, a biologist turned bioinformatician who somehow ended up spending as much time thinking about software, infrastructure, and data management as biology itself. Working in large research consortia and later leading a bioinformatics facility certainly helped along the way.

After more than two decades working in genomic, epigenomics, and biomedical research, I'm still learning, still catching up with new technologies, and still fascinated by the challenge of turning messy biological data into useful applicable knowledge.
