# Computing infrastructure & bioinformatic workflows

When people think about scientific computing infrastructure, they often think first about the compute cluster: CPUs, GPUs, storage capacity. But over the years, especially while running a bioinformatics core facility, I have come to think that the real challenge is not simply compute and store. It is designing an ecosystem where data, workflows, and users all fit together coherently.

The challenge is no longer simply:

> “Can we analyze this dataset?”

but increasingly:

> “Can we build a sustainable, reproducible, scalable ecosystem that allows many analyses, many users, and many projects to coexist efficiently over time?”

A modern bioinformatics core facility is no longer just a collection of Linux servers running analysis pipelines. It increasingly resembles a small scientific platform engineering organization, combining aspects of IT infrastructure, DevOps, software engineering, HPC, data management, scientific consulting and analysis. Unfortunately, many institutional managers still do not realize this and assume all of this can be carried by a team of two or three people.

Here I want to sketch out what I believe is a practical architecture for a modern bioinformatics core facility and explain how a typical workflow — differential gene expression analysis, from raw sequencing data to final report — fits into that infrastructure.

## Infrastructure components

A modern research institution requires a surprisingly diverse range of computational infrastructure:

-   desktops for administration and office work

-   laptops and tablets for electronic notebooks, presentations, teaching, and remote work

-   data storage systems

-   high-performance compute clusters

-   specialized equipment for imaging, sequencing, microscopy, and flow cytometry etc

-   interactive analysis platforms

-   backup and archival systems

-   networking and security infrastructure

-   cloud services and external data repositories

What is often underestimated is that all of these systems are increasingly interconnected. Modern biomedical research no longer consists of isolated instruments producing small local datasets analyzed on a single workstation. Instead, data continuously moves between instruments, storage systems, computational workflows, visualization platforms, external repositories, and collaborative environments.

A sequencing run may, for example, generate terabytes of data that need to be:

-   transferred securely,

-   validated,

-   processed on HPC infrastructure,

-   integrated with metadata,

-   analyzed through standardized workflows,

-   visualized interactively,

-   archived,

-   and eventually shared with collaborators or public repositories.

At the same time, researchers expect these systems to function seamlessly and often invisibly in the background

This creates a difficult balancing act between usability, performance, reproducibility, security, scalability, and long-term maintainability — often across infrastructures that were never originally designed to work together as a coherent system.

## The separation of concerns

One of the most important principles for network design is separating different types of traffic, responsibilities, and risks.

In practice this usually means the infrastructure is seperated into multiple logical network segments (VLANs or subnets):

| Segment                   | Purpose                                        |
|---------------------------|------------------------------------------------|
| User VLAN                 | researcher desktops, laptops, interactive work |
| Compute VLAN              | HPC compute nodes                              |
| Storage VLAN              | high-performance project storage               |
| Management VLAN           | infrastructure orchestration and monitoring    |
| DMZ / Transfer VLAN       | controlled data ingress/egress                 |
| Interactive Services VLAN | JupyterHub, RStudio, Open OnDemand             |

This separation is not just about security. It is also about performance and operational stability

## The data path

I have come to appreciate that one of the most common architectural mistakes is allowing sequencing data to flow through user desktops.

Large datasets should never follow this path:

Internet → laptop → project storage

Instead:

Internet → DMZ transfer node → validated ingest → project storage

The DMZ transfer node acts as a controlled gateway between the external world and the internal research environment. This is where:

-   Aspera

-   Globus

-   rsync

-   checksum validation

-   optional malware scanning

can take place. The compute cluster itself should generally have no direct internet access.

# Shared storage and scratch

Another important distinction is between persistent storage and temporary compute storage.

Persistent project storage contains:

-   raw FASTQs

-   references

-   metadata

-   final outputs

-   reports

-   archived results

This storage is collaborative, backed up, and long-lived.

Compute workflows, however, generate enormous amounts of temporary data:

-   alignment intermediates

-   sorting chunks

-   temporary BAMs

-   caches

-   decompression artifacts

Writing all of this directly to shared storage can easily overload the filesystem.

The standard solution is:

-   keep project data on shared storage

-   perform heavy intermediate computation on scratch storage

-   publish final outputs back to project storage

Conceptually:

project storage

↓

scratch staging (reference to input files)

↓

compute

↓

move results back to project storage

This model is particularly well aligned with workflow systems such as Nextflow.

------------------------------------------------------------------------

# Workflow orchestration and reproducibility

In times of the FAIR dogma and ISO certifications a modern bioinformatics facility (or for that matter any decent bioinformatician)  should treat workflows as production infrastructure rather than ad-hoc scripts.

For me this means:

-   version control

-   CI/CD

-   containers

-   automated testing

-   reproducible environments

-   provenance tracking

The workflows themselves live in:

-   GitLab or

-   lightweight alternatives such as Gitea

while the actual computation is orchestrated through:

-   Slurm

-   containers via Apptainer

-   standardized pipelines using Nextflow

This changes the mindset substantially.

The bioinformatics unit no longer simply “runs analyses”. It maintains a reproducible computational ecosystem.

------------------------------------------------------------------------

# Why Git infrastructure matters (this should be a seperate blog entry)

One topic I have become increasingly opinionated about is long-term sustainability of scientific software.

Many academic repositories disappear when:

-   teams dissolve

-   grants end

-   institute accounts are archived

-   key developers leave

For open-source workflows, I increasingly think the healthiest approach is:

-   internal institutional Git infrastructure for operational deployment

-   public neutral upstream repositories for long-term continuity

For example:

Internal GitLab

↕

Public GitHub organization

This allows:

-   institutional integration

-   CI/CD

-   controlled deployment

-   public sustainability

-   continued community contributions

without tying software survival to institutional restructuring.

------------------------------------------------------------------------

# Interactive analysis is changing

One of the biggest architectural shifts in recent years is the move away from “desktop-centric” bioinformatics.

Traditionally, users mounted institutional storage directly onto their laptops or desktops and ran local IDEs connected to remote systems.

Increasingly, institutes instead deploy:

-   JupyterHub

-   RStudio Server

-   VSCode Server

-   Open OnDemand

inside the infrastructure itself, close to compute and storage.

The user then interacts through a browser rather than directly moving data.

This has several advantages:

-   reduced data movement

-   fewer dependency conflicts

-   simpler onboarding

-   improved reproducibility

-   easier security governance

-   lower local hardware requirements

Most importantly, large datasets remain inside the institutional infrastructure.

Only:

-   rendered plots

-   notebook outputs

-   terminal streams

-   reports

cross to the user’s machine.

------------------------------------------------------------------------

# The hidden role of the management network

Users often do not see the management layer, but it is critical.

The Management VLAN typically contains:

-   authentication systems

-   monitoring

-   logging

-   scheduler controllers

-   configuration management

-   backup orchestration

-   CI/CD services

While scientific data flows primarily between:

-   storage

-   compute

-   interactive services

the management layer coordinates and supervises the entire ecosystem in the background.

In many ways it functions as the nervous system of the infrastructure.

------------------------------------------------------------------------

# Example: differential gene expression workflow

Putting this all together, a typical RNA-seq differential expression workflow might look something like this:

Public repository / GitLab

↓

Pipeline validated via CI/CD

↓

Data downloaded through DMZ transfer node

↓

FASTQs stored on project storage

↓

Nextflow launches jobs via Slurm

↓

Inputs staged to scratch

↓

Alignment / counting / DESeq2

↓

MultiQC aggregation

↓

Results published back to project storage

↓

Interactive exploration through RStudio/Jupyter

↓

Final Quarto/RMarkdown report

At this point the infrastructure itself starts becoming part of the scientific methodology.

------------------------------------------------------------------------

# Cloud and hybrid futures

An interesting aspect is that modern workflow-centric architectures are becoming increasingly portable between:

-   on-prem HPC

-   AWS

-   Azure

-   Kubernetes

-   hybrid infrastructures

The combination of:

-   containers

-   Nextflow

-   object storage

-   infrastructure-as-code

makes workflows much less tied to specific hardware.

I suspect many institutes will converge toward hybrid models:

-   stable routine workloads on-prem

-   burst scaling and AI/ML workloads in cloud environments

especially as GPU demand continues to grow.
