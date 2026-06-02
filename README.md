# Building Bioinformatics

**Practical lessons and best practices to help bioinformaticians build better software, create reproducible analyses, and develop sustainable research infrastructure.**

Bioinformatics has changed enormously over the last twenty years. What started as writing a few scripts to analyse biological data has evolved into managing large-scale datasets, complex workflows, cloud and HPC infrastructure, software projects, FAIR data systems, and increasingly, AI-driven analyses.

Like many bioinformaticians of my generation, I learned most of these skills 'on the go'. Few of us received formal training in software engineering, system administration, project management, or data architecture. We picked things up as we had to, usually while trying to solve immediate research problem.

The current generation of bioinformaticians is clearly better prepared. Dedicated bioinformatics, data science, machine learning, and computational biology programmes now cover topics that many of us had to learn independently. Yet gaps remain. While supervising students and early-career researchers, I've seen that important topics such as software engineering, reproducibility, project organisation, version control, and sustainable infrastructure are still often treated as secondary skills rather than core competencies.

This blog is where I collect notes, lessons learned, ideas, and practical solutions from years of working at the intersection of biology, data, and software. Some posts are tutorials, some are opinion pieces, and some are simply things I wish somebody had explained to me earlier in my career.

## Repository Structure

``` text
building-bioinformatics/
├── _quarto.yml
├── index.qmd
├── about.qmd
├── blog.qmd
├── notes/          # ideas, references, rough notes
├── drafts/         # work in progress
├── posts/          # published articles
├── assets/
│   ├── images/
│   └── css/
├── docs/           # rendered website (GitHub Pages)
└── .gitignore
```

## Writing Workflow

Most posts start life as notes. Ideas, references, diagrams, and rough thoughts go into the `notes/` folder. When a topic starts taking shape, it moves into `drafts/`. Once a post is ready for publication, it is moved to `posts/` and becomes part of the website.

The goal is to keep the thinking, drafting, and publishing stages separate while tracking everything in Git.

## Local Development

Preview the site locally (although I actually do this using POSIT formerly Rstudio):

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

After more than two decades working in genomics, epigenomics, and biomedical research, I'm still learning, still catching up with new technologies, and still fascinated by the challenge of turning messy biological data into useful knowledge.
