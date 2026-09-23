# How I Got from Scripts to Systems

*Ramblings of an ageing bioinformatician*

Like many bioinformaticians of my generation (and yes, it is the older one), I did not train to become one. I trained as a molecular biologist and acquired most of my computational skills while trying to solve actual research problems.

When I started my PhD in 2005, bioinformatics was already an established discipline. In fact, its roots reach back to the first computational analyses of protein sequences in the 1960's. But formal bioinformatics degrees and clearly defined career paths were much less common than they are today. People entered the field from biology, computer science, physics, mathematics or statistics and often learned what they needed as they went along.

That was certainly true for me.

During my PhD, I studied microsatellite evolution in yeast in a population genomics lab. I actually started by using Visual Basic to automate tasks in Excel. When the spreadsheets could no longer hold the data and the statistics became more complex, I turned to R, which I had first learned in ecology courses for statistical modelling. As the computational side of the project grew further, I learned Perl.

There was no particular plan behind this progression. I learned what I needed when I needed it.

Looking back almost twenty years later, this seems quite representative of how my skill set continued to develop. The questions changed, the technologies changed, and the scale changed. Each time, another layer was added.

## When the technology was still new

My transition into bioinformatics—and probably my reason for doing so—coincided with a major change in genomics.

The Human Genome Project had recently been completed, and new sequencing technologies were transforming the amount of biological data that could be generated. When I joined the CRG in 2009, RNA-seq was still very new. The first papers had appeared only shortly before, experimental protocols were becoming established, and there was not yet a mature analysis workflow that everyone simply followed.

We still had to work out how to analyse the data.

Questions that today have relatively established solutions—how to align reads, quantify expression, deal with transcript structures, compare samples and interpret the resulting measurements—were part of an actively developing methodological landscape. New algorithms and software appeared quickly, and choices made during analysis could substantially affect the result.

Working on transcriptomics and the ENCODE project during this period therefore meant more than applying existing tools. Understanding what they were doing, evaluating different approaches and deciding how to combine them were central parts of the work.

I encountered something similar later at CNAG when I started working with whole-genome bisulfite sequencing within BLUEPRINT. WGBS generated a different type and scale of sequencing data, and both the experimental protocols and computational approaches were still developing.

Across the field, methods for read alignment, genome assembly, transcript quantification, variant calling and many other tasks were developing rapidly. But as these individual analytical building blocks became more established, another problem became increasingly important:

**How do we execute the whole analysis reliably?**

## From scripts to workflows

A sequencing analysis is rarely a single program. Reads have to be checked, transformed, aligned or quantified; intermediate files are generated; samples have to be combined; statistical analyses follow; software versions and parameters matter.

At small scale, these steps can be connected with scripts and manual commands. At larger scale, that becomes increasingly fragile.

What happens when step eight of a twelve-step analysis fails? Can we restart without repeating everything? Which software version produced a particular result? Can somebody else run the analysis? Can I reproduce it myself six months later?

These are not primarily biological questions. But they directly affect the reliability of the biology.

During my time at CRG and particularly later at CNAG, pipelines became an increasingly important part of my work. GRAPE supported large-scale RNA-seq analysis; later, gemBS provided a structured pipeline for whole-genome bisulfite sequencing.

The pipelines I worked with were still largely implemented using Makefiles and Bash scripts. gemBS was experimentally implemented using CWL for ENCODE, but neither I nor the teams I worked with were routinely using systems such as Snakemake or Nextflow at that stage. These were emerging and would become much more widely adopted later.

The implementation has changed, but the underlying problem remains familiar: once the individual analytical steps are reasonably established, attention shifts towards connecting them and making the overall analysis run smoothly, repeatedly and at scale.

The analysis itself becomes only one part of a larger computational process.

## From workflows to systems

At CNAG, I encountered this at yet another level.

A large sequencing centre is a production environment. High-throughput projects do not begin and end with the bioinformatics pipeline. Samples, laboratory protocols, biobanking, metadata, sequencing, computational processing and data delivery have to fit into a coordinated process. A LIMS connects information across that process, while established laboratory protocols and production pipelines make it possible to handle large numbers of samples consistently.

This was quite a different perspective from working on an individual research analysis. The question was no longer only whether an analytical method worked, but how it fitted into a larger process that had to work repeatedly and at scale.

When I later led a bioinformatics core facility at IJC, I encountered the same problem from almost the opposite direction. Instead of entering an established sequencing environment, my team and I had to build many of these structures from scratch for a much smaller and more heterogeneous setting.

There were different projects, researchers and data types, all with different requirements. Projects needed sufficient metadata. Analyses needed to run consistently. Results had to be stored and communicated. Software had to be maintained. People needed documentation and training. Computational resources had to be organised.

For methylation-array projects, for example, we developed an environment in which BioForms captured project and sample information, EPipe automated the analysis, computational resources handled the processing, and MethylationDB provided structured access to results.

None of these components alone was the bioinformatics analysis. The useful system emerged from connecting them.

This changed how I thought about bioinformatics. Increasingly, the object I was working on was not only the analysis, but also the **system around the analysis**.

## A skill set that accumulated

This is also how I have come to think about the changing skill set of bioinformatics: not as one set of skills replacing another, but as an accumulation of layers.

**[FIGURE: From scripts to systems — technological milestones and the evolving bioinformatics skill set]**

Biological knowledge did not become less important when programming became important. Scripting did not disappear when workflow managers arrived. Statistical genomics remains fundamental even as machine learning becomes more common.

Instead, new capabilities were added.

High-throughput sequencing required new algorithms and scalable computing. Increasingly complex analyses brought workflow management, version control and software-engineering practices. Reproducibility connected analysis more closely with documentation and data management. Multi-omics, single-cell and spatial technologies created new integration problems. Machine learning and deep learning added another methodological layer.

As all these components became interconnected, understanding the wider computational ecosystem also became increasingly useful.

The important point in the figure is that the earlier skills do not end when a new one appears.

They accumulate.

## There is no single modern bioinformatician

There is an obvious problem with presenting the field this way.

Taken together, the figure starts to look suspiciously like a job advertisement for an impossible person: molecular biologist, statistician, programmer, software engineer, data engineer, infrastructure specialist and machine-learning expert all at once.

That is not the point (although those job advertisements exist).

As bioinformatics has expanded, specialisation has become both possible and necessary. Some bioinformaticians work close to biological interpretation and statistical modelling. Others specialise in methods development, scientific software, workflows, research data, computational infrastructure or machine learning.

Perhaps the important change is not that every bioinformatician needs all these skills, but that modern bioinformatics increasingly depends on **all these capabilities existing somewhere within the team or organisation**.

We also need enough understanding of neighbouring areas to work across their boundaries.

## Starting from a different place

Students entering bioinformatics today start from a very different position than I did.

An undergraduate bioinformatics curriculum can now include molecular and cell biology alongside programming, algorithms, databases, biostatistics, statistical learning, computational genomics, machine learning and high-performance computing.

That breadth would have been difficult to imagine when I moved from molecular biology into computational work.

But completing a course is not quite the same as dealing with the corresponding problem in practice.

Learning programming is different from maintaining software that other people depend on. Learning statistics is different from deciding what to do with a difficult experimental dataset. Learning about workflows is different from debugging one that has failed after processing hundreds of samples. And learning about reproducibility is different from trying to reproduce an analysis years later when the software, operating system and people involved have all changed.

Formal education provides a much stronger starting point today. Experience still provides something different.

Many of the skills that have mattered most in my own career developed through applying them to real problems, getting things wrong, debugging them and eventually recognising patterns in the problems that kept appearing.

## And now AI changes the interface again

And now we are adding another layer.

Generative AI is changing how we interact with computational tools. Code can be generated from natural-language descriptions, unfamiliar libraries can be explored much more quickly, and AI systems are beginning to connect tools and execute parts of computational workflows.

This lowers another technical barrier.

But making something easier to execute does not necessarily make it easier to judge.

Is the analysis appropriate for the biological question? Is the generated code correct? Are the assumptions reasonable? Can the results be validated and reproduced? And what happens when an AI-generated solution is perfectly plausible and wrong?

Truong and Ritchie describe the current shift as one in which scientific intent, verification and computational critical thinking become increasingly important. I find that a useful way of looking at it.

AI may well reduce the amount of time we spend writing certain kinds of code. It seems much less likely to reduce the need to understand what an analysis is doing, how its components fit together, or whether the result makes biological sense.

## From scripts to systems

Looking back, I never made a conscious decision to move from scripts to systems.

I started with biological questions. Those questions led me to data, statistics and programming. Larger datasets led to pipelines and scalable computing. Repeated analyses made reproducibility and workflow management important. Working in a sequencing centre showed me what large-scale production looks like. Building a bioinformatics facility made me think about how data, software, infrastructure and people fit together.

Each layer appeared because the previous one was no longer enough on its own.

Perhaps that is why defining the skill set of a bioinformatician has become so difficult. Bioinformatics sits at a boundary that keeps moving as biology and technology change.

The tools will continue to change. The ability to understand the biological problem, learn what is needed to address it, and connect the necessary pieces into something that works seems rather more durable.
