---
title: "Introduction"
teaching: 30
source: md
questions:
- "How to setup Nanopore Sequencing?"
- "What is the format of NGS sequencing data?"
- "What are things commonly encountered in NGS data processing and bioinformatics?"
objectives:
- "Understand how to setup a Nanopore sequencing run"
- "Understand the format of ONT sequencing data"
- "Understanding NGS data processing"
---

### NGS Workflows
When working with NGS sequencers, we feed it with a DNA library, and obtain raw read data off of the sequencer. This raw data often cannot be used directly, and will typically need to pass through a number of tools before we can obtain our desired output. The execution of this set of tools in a specified order is commonly referred to as a *workflow* or *pipeline*. However, there is usually no "One Size Fits All" workflow, as different applications and projects will likely require different tools and hence *workflows*. However, there will often be commonalities between each *workflow*, such as how many *workflows* might require or work with seqeunce alignment data.

One of the most common and basic uses of the Nanopore sequencer in our lab involves 1) Plasmid De novo Assembly, and 2) Alignment to a Reference Sequence/Genome. This processes from the start to end can be represented as a basic *workflow* shown in the image below. 

![Basic Workflow](../fig/MinKNOW/6.png)

In the *workflow* shown above, it can be mainly divided into two segments. First is the sequencing stage, which will be handled by the MinKNOW UI application. Next is the analysis stage, which is where most of the bioinformatics is involved. In this segment, we will go through the run parameters users should be aware and concerned of within MinKNOW so that they can maximise their throughput, and at the same time ensure that they are getting what they need from the sequencing run.

### MinKNOW


