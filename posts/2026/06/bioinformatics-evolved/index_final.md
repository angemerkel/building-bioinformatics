---
title: "A Bioinformatics Core Is More Than a Cluster"
subtitle: "The real challenge is building a sustainable bioinformatics ecosystem."
description: "A practical look at the infrastructure behind modern bioinformatics, from data ingestion and storage to workflow orchestration, reproducibility, and platform engineering."
date: 2026-07-16
author: "Angelika Merkel"
categories:
  - Bioinformatics
  - Research Computing
  - Infrastructure
draft: true
---

When people think about scientific computing infrastructure, they often think first about the compute cluster: CPUs, GPUs and storage capacity.

But over the years, and especially while running a bioinformatics core facility, I have come to think that the real challenge is not simply providing enough computing power and storage. It is building an ecosystem in which data, workflows, infrastructure and users fit together coherently.

The question is no longer simply:

> Can we analyse this dataset?

but increasingly:

> Can we build a sustainable and reproducible environment in which many analyses, users and projects can coexist efficiently over time?

A modern bioinformatics core facility is much more than a collection of Linux servers running analysis pipelines. It combines aspects of research computing, data management, software engineering, workflow orchestration, reproducibility and scientific support. In practice, however, this breadth of responsibility is not always reflected in how bioinformatics units are staffed.

In use this post, I want to sketch out what I believe is a practical architecture for a modern bioinformatics core facility and follow a typical workflow through it, from the arrival of raw sequencing data to computation, analysis and eventually the results that are returned to researchers.

This is not meant as the architecture every institute should implement. Different organisations have different requirements, resources and existing infrastructure. Rather, it reflects some of the principles I have found useful when thinking about how data, workflows, infrastructure, reproducibility and people fit together into a sustainable scientific system.

## The data path

Before we can analyse anything, the data has to get into the infrastructure.

Research computing environments are often divided into different network segments, or VLANs, separating user devices, compute resources, storage, management systems and services exposed to external networks.

![Schematic network architecture for a bioinformatics computing environment.](images/Network_architecture.png)

This separation is partly about security, but it can also help separate different types of traffic and responsibilities and improve operational stability. For a bioinformatics workflow, these infrastructure decisions become very practical as soon as large datasets have to be transferred.

For smaller files, downloading data to a laptop and subsequently copying it to project storage may be little more than inefficient. For hundreds of gigabytes or terabytes of sequencing data, it quickly becomes impractical.

Rather than moving large datasets through a user's computer:

***Internet → laptop → project storage***

a research infrastructure may provide a dedicated transfer node:

***Internet → DMZ transfer node → validated ingest → project storage***

A demilitarised zone, or DMZ, provides a controlled network area between external networks and the internal institutional infrastructure. A transfer node within this environment can act as a gateway for incoming and outgoing research data, with firewall rules and access controls appropriate for that role.

This is where tools such as Aspera, SFTP, `wget` or `curl` can be used, together with checksum validation before data are moved into persistent project storage.

For example, downloading sequencing data from the European Nucleotide Archive might look something like this:

```bash

# Connect to the transfer node
ssh -i ~/.ssh/id_ed25519 username@transfer01.institute.org

# Download to the ingest/staging area
wget \
  -P /dmz/ingest/PROJECT_X/ \
  https://ftp.sra.ebi.ac.uk/vol1/fastq/ERR123/ERR123456/ERR123456_1.fastq.gz

# Validate the downloaded files
md5sum -c checksums.md5

# Move validated data to project storage
rsync -avP \
  /dmz/ingest/PROJECT_X/ \
  /data/projects/PROJECT_X/raw/
```

The exact tools depend on where the data come from and how large they are. What matters is that the transfer method is appropriate for the dataset and that enough capacity exists not only in the final project storage, but also in any temporary staging area used along the way.

