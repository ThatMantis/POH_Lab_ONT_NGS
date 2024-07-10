---
title: "7. Variant Calling"
teaching: 90
source: md
questions:
- "What is variant calling?"
- "How to perform variant calling?"
objectives:
- "Understand how to perform variant calling."
---

After the conducting the Demultiplexing and QC steps from above, the next step in the workflow will be to do an alignment of the demultiplexed (and QC-ed) .Fastq files against the reference gene of interest sequence. For this step, we can rely on the `Custom Fastq Alignment` workflow in EPI2ME to do the alignment for us, so that we can have one less thing to be concerned about optimising :) . For this workshop, alignment has been pre-run on EPI2ME, and the .bam and .bai files may be found in the `./vc/epi2me` directory. We will use those files for the rest of this exercise.

### Variant Calling.
