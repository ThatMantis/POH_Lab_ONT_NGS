---
title: "EPI2ME"
teaching: 30
source: md
questions:
- "How to process ONT data?"
objectives:
- "Learn the methods available to process ONT data."
- "Processing ONT data in the simplest manner with GUI programs from ONT."
---

### Data Processing With GUI Programs

Now that (assuming) we have sequenced our DNA samples on the Nanopore Sequencer, we will probably need a method to analyse the data output (unless looking at thousands of lines of FASTQ output manually is your thing!). Typically to get useful information out of our sequencing data, the raw reads will need to pass through a variety of tools to give us our desired output -- aka a *workflow* or *pipeline*. Most of these *workflow* or *pipeline* will require some coding and work on the command line. However, there are also programs out there which require minimal coding and work on the command line by allowing the user to interact with Graphical User Interfaces (GUIs) -- these programs typically have the *workflow/piplines* hidden in the background behind the fancy looking GUIs, so that it looks less daunting to users with minimal coding experiences and are uncomfortable with using command line approaches, and who just want to get the work done.

One such GUI program is the EPI2ME suite of applications, maintained by EPI2ME labs that offers a collection of [Nextflow] based bioinformatics workflows tailored to Oxford Nanopore Technologies (ONT) long-read sequencing data. In this chapter, we will take a look at EPI2ME, and how we might use them in our lab.

![EPI2ME](../fig/EPI2ME/2.png)

ONT currently offers two versions of EPI2ME. Shown on the left is the *EPI2ME Agent*, an older client which is meant to be retired end May 2024 (but somehow still works at the time of writing, June 2024). Whereas shown on the right is the *EPI2ME Desktop* program, which is meant to replace *EPI2ME Agent*. *EPI2ME Agent* makes use of cloud based computing for processing the workflows (AWS), which means anyone can use it regardless of their computer's capabilities. Whereas *EPI2ME Desktop* offers both cloud and local compute, although at the time of writing in June 2024, for most users it is currently limited to local compute, with cloud access limited to certain users only in closed beta.

For the remaining portions of this chapter, we will look at how we can use the EPI2ME programs for some of the most common use cases in our lab:
- De novo sequence assembly: Can be used to de novo assemble plasmid sequences etc. from the FASTQ sequencing data.
- - Note: Only samples containing a singular plasmid should use this analysis on EPI2ME! If your sample contains more than one plasmid, it is best to do a custom alignment specific to the plasmid we are interested at looking.
- Custom Alignment: Can be used to align our sequencing data to a reference sequence. This step is useful for much of other workflows too!

### EPI2ME Agent

> ## Scheduled to be discontinued
>
>  Note that this segment of the website will be removed once service on the *EPI2ME Agent* is confirmed to be officially discontinued, and thus not relevant!
> 
{: .warning}

In this segment, we will look at the use of the *EPI2ME Agent* for the two use cases mentioned above; which relies only on cloud based computing, making it possible for anyone to "run" their analysis on any computer.

![EPI2ME Workflows](../fig/EPI2ME/3.png)

#### De novo Plasmid Assembly

Starting from the *EPI2ME Agent's*"homepage", first press `New Analysis`, followed by `Select Folder(s)` to select the folder(s) containing the **BASECALLED** sequencing data -- This should be taken from the `"/fastq_pass"` folder! Select those folders and press on `Next` to select the workflow we will be running.

![Denovo01](../fig/EPI2ME/denovo01.png)

Here we will select `Fastq Clone Validation`, and press `Next`.

![Denovo02](../fig/EPI2ME/denovo02.png)

Select `No` to the option "Are you uploading human DNA/RNA?". We should then see this screen. Thereafter, we will enter the estimated size of the plasmids we are expecting. This should be a value not more or less than 50% of the value indicated here. If you have samples with sizes much smaller than 50% of the value or 150% of the value indicated here, it will be best to rerun the analysis for those samples seperately in a seperate analysis!

![Denovo03](../fig/EPI2ME/denovo03.png)

Once the workflow starts, we should see a screen like this. Just leave the computer ON and let the program do its thing! This stage can take quite a while, depending on network and how long it takes to upload the files onto the cloud.

![Denovo04](../fig/EPI2ME/denovo04.png)

Once the analysis is completed, we can `Stop` the `Upload` and `Anlysis` buttons on the top of the screen. We should see something like this. The results of succesful De novo assemblies are indicated as `Completed succesfully` under `Status`, whereas those which failed will be indicated as `Failed to ...`. The reasons for failure can vary, but usually it means there might be something wrong with our plasmid sample! It will be best to reanalyse through a custom alignment for the failed samples later on!

![Denovo05](../fig/EPI2ME/denovo05.png)

To access the output, scroll down from the screen above and click on `output`.

![Denovo06](../fig/EPI2ME/denovo06.png)

This should open up a File Explorer tab where all the EPI2ME analysis are stored by default. Find the folder with the corresponding `Analysis ID`.

![Denovo07](../fig/EPI2ME/denovo07.png)

In the folder with the corresponding `Analysis ID`, we should find the *.fasta* files for the samples where De novo assembly was succesfull. We can then take these *.fasta* files and upload them to benchling/BLAST etc for alignment!

![Denovo08](../fig/EPI2ME/denovo08.png)

#### Custom Alignment

[Nextflow]: https://www.nextflow.io/
