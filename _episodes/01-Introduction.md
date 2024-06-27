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

In the *workflow* shown above, it can be mainly divided into two segments. First is the sequencing stage, which will be handled by the MinKNOW UI application. Next is the analysis stage, which is where most of the bioinformatics is involved. In this segment, we will go through the run parameters users should be aware and concerned of within MinKNOW so that they can maximise their throughput, and at the same time ensure that they are getting what they need from the sequencing run. Note that here we will mainly be talking about the Flongle flowcell, used with a MINion Mk1b Sequencer.

### MinKNOW

The MinKNOW UI is the software that drives and controls the Nanopore Sequencing devices. It controls the sequencer with the run parameters set by the user, and handles data acquisition from the seqeuncer, and allows for real-time analysis and feedback. Here, we will be concerned with two of the functions available in the MinKNOW UI -- namely the "*Flow Cell Check*" and the actual Sequencing, through the "*Start Sequencing*" function. These can be accessed through the "*Start*" page tab.

![MinKNOW UI Functions](../fig/MinKNOW/2.png)

#### Flow Cell Check

The flow cell check is a vital function that should be performed prior to the loading of DNA Library into any flow cell, and the start of any sequencing run. The flow cell check verifies the condition of the flow cell, ensuring that there are sufficient pores available for sequencing, and highlights to the experienced user any possible issues with the flow cell. So as to reduce unnecesssary trouble that might arise from loading and starting a run on a "bad" flow cell. To start a flow cell check, simply click on the "*Flow Cell Check*" button from the "*Start*" tab page shown above. This will then bring us to the next page where we can:
- Enter the Flow cell ID
- Select the Flow cell type (typically *FLO-FLG114* for our lab as of June 2024)

![Flow Cell Chk 01](../fig/MinKNOW/chk01.png)

Pressing the "*Start*" button will begin the flow cell check, where after a short approx 10-15 minutes wait, we will get either one of two possible results, shown below in their respective orders:
- Flow cell check ***PASSED***
  - This signifies the flow cell check has passed, and the flow cell has at least 50 (out of 126) pores available. Users can proceed with loading their library and starting the run as per normal

![Flow Cell Chk 02](../fig/MinKNOW/chk02.png)

- Flow cell check ***FAILED***
  - This signifies the flow cell check has failed, as there are fewer than 50 (out of 126) pores available per flow cell.
  - However, this does not immediately suggest the flow cell is unusable and should be discarded. Users should consider the following and proceed based on their own discretion.
      - IF above 30 pores, and a high throughput is not exactly needed: users might be able to proceed.
      - IF below 30 pores, and/or a high throughput is required: users should change to a different, new flow cell.
- 
![Flow Cell Chk 03](../fig/MinKNOW/chk03.png)
