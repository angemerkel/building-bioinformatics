# How I Got from Scripts to Systems

*The changing skill set of the bioinformatician*

Like many bioinformaticians of my generation, I did not train to become one. I trained as a molecular biologist and acquired most of my computational skills while trying to solve actual research problems.

When I started my PhD in 2005, bioinformatics was already an established discipline. In fact, tts roots reach back to the first computational analysis of protein sequences in the 1960s, long before genomics or next-generation sequencing. But formal bioinformatics degrees and clearly defined career paths were much less common than they are today. People entered the field from biology, computer science, physics, mathematics or statistics and often learned what they needed as they went along.

That was certainly true for me.

During my PhD, I studied microsatellite evolution in yeast in a population genomics lab. This involved scanning whole genomes with tandem-repeat detection algorithms, benchmarking the results and developing the computational processing around them. I actually started by using Visual Basic to automate tasks in Excel. When the spreadsheets could no longer hold the data and the statistics became more complex, I turned to R, which I had first learned in ecology courses for statistical modelling. Eventually, as the computational side of the project grew further, I learned Perl.

There was no particular plan behind this progression. I learned what I needed when I needed it.

Looking back almost twenty years later, this seems quite representative of how my own skill set continued to develop. The questions changed, the technologies changed, and the scale changed. Each time, another layer was added.

## When the technology was still new

The timing of my transition into bioinformatics (and problably my reson to do so) coincided with a major change in genomics.

The Human Genome Project had recently been completed, and new sequencing technologies were beginning to transform the amount of biological data that could be generated. The first commercial next-generation sequencing platforms appeared in the mid-2000s. Over the following years, sequencing throughput increased dramatically and the bottleneck increasingly moved from generating data towards analysing it.

When I joined the CRG in 2009, RNA-seq was still very new. The first RNA-seq papers had only appeared shortly before, and experimental protocols were just becoming established. There was not yet a mature, standard analysis workflow that everyone simply followed.

We still had to work out how to analyse the data.

Questions that today have relatively established solutions—how to align the reads, quantify expression, deal with different transcript structures, compare samples and interpret the resulting measurements—were part of an actively developing methodological landscape. New algorithms and software appeared quickly, and choices made during the analysis could substantially affect the result.

Working on transcriptomics and the ENCODE project during this period meant that bioinformatics was not simply about applying existing tools. Understanding what the tools were doing, evaluating different approaches and deciding how to combine them were central parts of the work.

The same happened again when I later moved to CNAG and started working with whole-genome bisulfite sequencing within BLUEPRINT. WGBS generated a different type and scale of sequencing data, and both the experimental protocols and the computational approaches were still developing. Again, part of the work was figuring out how the data should be processed and analysed in the first place.

Across the field, this period saw the development and rapid evolution of many of the algorithms and tools that now form the basis of sequencing-data analysis: methods for read alignment, genome assembly, transcript quantification and variant calling, among others.

But another problem was becoming increasingly visible at the same time.

Once we knew how to perform an analysis, we also had to think about **how to execute it reliably**.

## From scripts to workflows

A sequencing analysis is rarely a single program. Reads have to be checked, transformed, aligned or quantified; intermediate files are generated; results from multiple samples have to be combined; statistical analyses follow; software versions and parameters matter.

At small scale, it is possible to connect these steps with scripts and manual commands. At larger scale, that becomes increasingly fragile.

What happens when step eight of a twelve-step analysis fails? Can the analysis restart without repeating everything? Which version of a tool produced a particular result? Can somebody else run the same analysis? Can I reproduce it myself six months later?

These are not primarily biological questions. But they directly affect the reliability of the biology.

During my time at CRG and particularly later at CNAG, pipelines therefore became an increasingly important part of my work. GRAPE was developed to support large-scale RNA-seq analysis; later, gemBS provided a structured pipeline for processing whole-genome bisulfite sequencing data.

At that stage, however, the pipelines I worked with were still largely implemented using Makefiles and Bash scripts rather than the workflow-management systems that are common today. gemBS was experimentally implemented using CWL for ENCODE, but neither I nor the teams I worked with were yet routinely using systems such as Snakemake or Nextflow. These were emerging at around the same time and would later become much more widely adopted.

This was part of a broader transition in bioinformatics: from connecting tools with scripts and Makefiles towards more explicit workflow management and reproducible computational environments. Version control made changes to code traceable, containers addressed software dependencies and portability, and tools such as R Markdown and Jupyter brought analysis, code and documentation closer together.

The individual technologies are less important than the problem they were trying to solve.

The analysis itself was becoming only one part of a larger computational process.

## From workflows to systems

At CNAG, I also encountered this at another level. A large sequencing centre is a production environment. High-throughput projects do not begin and end with the bioinformatics pipeline. Samples, laboratory protocols, biobanking, metadata, sequencing, computational processing and data delivery all have to fit into a coordinated process. A LIMS connects information across that process, while established laboratory protocols and production pipelines make it possible to handle large numbers of samples consistently.

This is a different perspective from working on an individual research analysis. The important question is no longer only whether an analytical method works, but how it fits into a larger process that had to work repeatedly and at scale.

When I later led a bioinformatics core facility at IJC, I encountered the same problem from almost the opposite direction. Instead of entering an established sequencing environment, I had to think about how to build many of these structures from scratch for a much smaller and more heterogeneous setting.

There were multiple projects, researchers and data types, each with different requirements and different levels of computational expertise. Projects needed to arrive with sufficient metadata. Analyses needed to run consistently. Results had to be stored and communicated. Software needed to be maintained. People needed documentation and training. Computational resources had to be organised.

For methylation-array projects, for example, my team (we) developed an environment in which BioForms captured project and sample information, EPipe automated the analysis, computational resources executed the processing, and MethylationDB provided structured access to results. None of these components alone constituted the bioinformatics analysis. The useful system emerged from connecting them.

This changed how I thought about bioinformatics.

The object I was working on was no longer only the analysis. Increasingly, it was also the **system around the analysis**.

That does not mean that every bioinformatician needs to become a systems engineer. But it does mean that systems thinking has become relevant to a much larger part of bioinformatics than it once was.

## A skill set that accumulated

One way of looking at the evolution of bioinformatics over the last twenty-five years is therefore not as a succession of skills replacing one another, but as an accumulation of layers.

**[FIGURE: From scripts to systems — technological milestones and the evolving bioinformatics skill set]**

Biological knowledge did not become less important when programming became important. Scripting did not disappear when workflow managers arrived. Statistical genomics remains fundamental even as machine learning becomes more common.

Instead, new capabilities were added.

The rise of high-throughput sequencing required new algorithms for alignment, quantification, variant calling and genome assembly. Increasing data volumes required HPC, cloud computing and other forms of scalable computing. More complex analyses increased the need for workflow management, version control and software-engineering practices. Reproducibility brought analysis, documentation and data management closer together. Multi-omics and later single-cell and spatial technologies created increasingly complex data-integration problems. Machine learning and deep learning added another methodological layer.

And as these components became interconnected, understanding the wider computational ecosystem—and how to design the infrastructure around it—became increasingly useful.

The important point is that the arrows in the figure all continue to the present.

New technologies have not removed the need for the earlier skills.

## There is no single modern bioinformatician

There is an obvious problem with presenting the field this way.

Taken together, the figure can easily start to look like a job advertisement for an impossible person: molecular biologist, statistician, programmer, software engineer, data engineer, infrastructure specialist and machine-learning expert all at once.

That is not the point (although the job advertisements exist).

As bioinformatics has expanded, specialisation has become both possible and necessary. Some bioinformaticians work close to biological interpretation and statistical modelling. Others specialise in methods development, scientific software, workflow engineering, research data, computational infrastructure or machine learning.

The important change is perhaps not that every bioinformatician needs all these skills, but that modern bioinformatics increasingly depends on **all these capabilities existing somewhere within the team or organisation**.

It also means that we need enough understanding of neighbouring areas to work across their boundaries.

## Starting from a different place

Students entering bioinformatics today start from a very different position than I did.

A current undergraduate bioinformatics curriculum can include molecular and cell biology alongside several programming courses, algorithms, databases, biostatistics, statistical learning, computational genomics, machine learning and high-performance computing.

That breadth would have been difficult to imagine when I started moving from molecular biology into computational work.

But there is also a danger in interpreting a curriculum as a list of skills that someone possesses after completing the corresponding course.

Learning programming is not the same as maintaining software that other people depend on. Learning statistics is not the same as deciding what to do with a difficult experimental dataset. Learning about workflows is different from debugging one that has failed after processing hundreds of samples. And learning the principles of reproducibility is different from trying to reproduce an analysis several years later when the software, operating system and people involved have all changed.

Formal education provides a much stronger starting point today. Experience still provides something different.

Many of the skills that have mattered most in my own career developed through applying them to real problems, getting things wrong, debugging them, discussing them with colleagues and eventually recognising patterns in the problems that kept appearing.

## And now AI changes the interface again

We are now adding another layer.

Generative AI and large language models are rapidly changing how we interact with computational tools. Code that once required considerable programming experience can now be generated from a natural-language description. Documentation can be queried conversationally. Unfamiliar libraries can be explored much more quickly. Increasingly, AI systems can connect tools and execute parts of computational workflows.

This lowers another technical barrier, just as graphical interfaces, web servers and workflow systems lowered barriers before it.

But making something easier to execute does not necessarily make it easier to judge.

Is the analysis appropriate for the biological question? Are the assumptions reasonable? Is the generated code correct? Are the results reproducible? Can they be validated? How does the analysis fit into the wider computational environment? And what happens when an AI-generated solution is plausible but wrong?

Truong and Ritchie describe this as a shift in the bottleneck from technical execution towards scientific intent, verification and computational critical thinking.

I find that a useful way of thinking about the current moment.

Perhaps AI will reduce the amount of time bioinformaticians spend writing certain kinds of code. It seems much less likely to reduce the need to understand what the analysis is doing, how its components fit together, or whether the result makes biological sense.

## From scripts to systems

Looking back, I never made a conscious decision to move from scripts to systems.

I started with biological questions. Those questions led me to data, algorithms and programming. Larger datasets led to pipelines and scalable computing. Repeated analyses led to workflow management and reproducibility. Running a facility forced me to think about data, software, infrastructure and people as parts of the same environment.

Each layer appeared because the previous one was no longer enough on its own.

That may also explain why defining the skill set of a bioinformatician has become increasingly difficult. Bioinformatics sits at a boundary that keeps moving as biology and technology change.

The tools will continue to change. The ability to understand the biological problem, learn what is needed to address it, and connect the necessary pieces into something that works remains rather more durable.
