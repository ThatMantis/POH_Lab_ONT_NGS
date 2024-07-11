---
title: "8. Assembly"
teaching: 90
source: md
questions:
- "How to assemble an unknown sequence from scratch?"
objectives:
- "Understand how to assemble an unknown sequence from scratch."
---

### Exercise 2

As we come to the end of today's workshop, we will end it off by doing a "fun exercise" which will also serve as a summary and recap of the contents taught in the previous chapters today. :)

In the imaginary scenario of this exercise, we came across/were given a bacteria strain that performs exceptionally well for our intended application. However, we are unable to identify what strain of bacteria this is, and what are the specific genes and mutations present in this bacteria that enables it to perform the way it does. While we can do 16S rDNA and 18S rDNA sequencing to obtain the taxonomic classification of the cell, it still doesn't give us the information we need to know about its genotype.

To solve our imaginary problem, we will need to sequence and conduct a genome assembly. To do so, we first lysed the wild-type cell and obtained the genomic DNA of the cell using a genomic DNA purification kit. We then sheared the genomic DNA into linear fragments through mechanical means, and prepared the DNA for sequencing using a ligation sequencing kit. The prepared library was then loaded into a Flongle R10 flow cell, sequenced and basecalled through the MinKNOW app with Super-High Accurary settings, and filtered for a minimum Qscore of 10. The raw basecalled sequencing files can be found in `~/ngs_workshop/assembly/fastq_pass`. The workflow for a general genome assembly/DNA sequence assembly is depicted in the image below.

![Generic assembly workflow](../fig/Assembly_workflow.png)

### Step 1. Quality Control

As this DNA library was prepared and sequenced without the use of any barcoding kits/barcodes, we will move on directly to the quality control step of the workflow. We will use [FastQC] to assess the read quality. But before we do that, lets first merge all the individual .fastq files into a single file so as to make our life easier! (there are 200+ files because by default, MinKNOW saves the basecalled output into a new FastQ file every ~10 minutes).

~~~
# Lets first make sure we are in the right directory
cd ~/ngs_workshop/assembly/fastq_pass

# And then create a new directory to store our merged fastq file, so as to minimise any potential hiccups that might occur when we recursively go through all the fastq files later in this directory
mkdir merged

# We will now merge ALL the raw .fastq files into one .fastq file into the ./merged directory, using "cat" -- short for "concatenate", which is pre-installed in most linux platforms
# We will name the output file "R10_BL21.fastq.gz" (or whatever you want!)
cat *.fastq.gz > ./merged/R10_BL21.fastq.gz

# (Optional) We will now go into the ./merged directory, and unzip the .fastq.gz file
cd merged
gunzip -k *.gz
~~~
{: .bash}

We will now run FastQC on this merged .fastq file! We can either simply enter `fastqc` into the command line and generate the report through the GUI application. Or generate the report through the command line. Here we will show again how to generate the report through the command line. We can use either .fastqc or compressed .fastqc.gz file as input. We have omitted the `-o` parameter choose and decided to simply store the FastQC report in the existing directory. Due to the relatively larger size of this .fastq file compared to the one we used for variant calling, we added a `-t 2` parameter to increase the processing thread count and hence increasing the total memory that can be allocated for processing this larger .fastq file (we can increase the thread count appropriately as needed, but we should take note not to run more threads than our available memory! In particular not more than 6 threads on a 32 bit machine!). 

~~~
fastqc R10_BL21.fastq  -t 2
~~~
{: .bash}

> ## Generate a QC report with PycoQC!
>
> We can also generate a QC report with PycoQC just for fun! 
>
> > ## Solution
> >
> > ~~~
> > # Go to the directory containing the sequencing_summary.txt file
> > cd ~/ngs_workshop/assembly
> > # Generate the PycoQC report
> > pycoQC -f sequencing_summary_ATH727_a2b50ed3_b9fd1fba.txt -o R10_BL21_pycoQC.html
> > ~~~
> > {: .bash}
> >
> {: .solution}
> 
{: .challenge}

Lets take a look at the QC reports!

### Step 2. Filtering

Since we can see that the head quality indeed is of lower quality. Lets do some head and tail cropping of the reads, since we are doing long read sequencing here and can afford to! We will crop the head and tail 150bp, which is generally the region historically [reported to be of relatively lower quality]. To do so, we will use the program [nanofilt]. `--headcrop 150 --tailcrop 150` crops the first and last 150bp of each read, `-l 2000` filters out reads shorter than 1000 bp. Lets also try `-q 15` to filter off reads with Qscore below 15. `> R10_BL21_trimmed.fastq` pipes and saves the output into "R10_BL21_trimmed.fastq"; else NanoFilt will spit the output directly onto the command line -- try it for fun!

~~~
NanoFilt R10_BL21.fastq -q 13 -l 1000 --headcrop 150 --tailcrop 150 > R10_BL21_trimmed.fastq
~~~
{: .bash}

Now lets run FastQC again on the trimmed.fastq file. We should now see that the mean of the "Per Base Sequence Quality" is now all in the "green"!

### Step 3. Assembly

(Genome) assembly is the process of putting together your reads, short-reads, long-reads or both, into long contiguous sequences (contigs). Again as with everything else, many programs are available for assembly. EPI2ME's Clone Validation Workflow (for plasmid de novo assembly) uses [flye] by default and offers [canu] as an alternative. Both are very capable assemblers, canu requires much more computational resources to run, and will likely exceed the time available in this workshop to run. Hence, we will explore flye here instead.

Due to the dependencies required for flye, we will install flye into a new conda environment, as follows:

~~~
# new environment created with name "flye"
conda create --name flye -c conda-forge -c bioconda flye 
~~~
{: .bash}

Thereafter, we can change into the "flye" environment with `conda activate flye`. We can then run flye on the NanoFilt filtered reads! `--nano-hq ./R10_BL21_trimmed_q15.fastq` Specifies the input file, and `--nano-hq` specifies that the reads are of relatively higher quality (requirements are reads basecalled using **Super-Accurate Basecalling**, and **<5% error** -- both of which we (almost) fulfilled, since we NanoFilt filtered at Qscore 13). `--genome-size 4.5m` specifies that we expect the assembly to be about 4.5 million bp (e.coli). `--threads 4` specifies that we will use 4 threads for computing power to speed up the process. `--iterations 3` specifies that we want to polish the assembly 3 times (for better accuracy). `--out-dir ./flye_output` specifies the output we want to store the flye assembled output and temporary files in. The final assembled .fasta file is `assembly.fasta`. This step may take a while to run.

~~~
# Create a new directory to store the flye-assembled output
mkdir flye_output
flye --nano-hq ./R10_BL21_trimmed.fastq --genome-size 4.5m --threads 4 --iterations 3 --out-dir ./flye_output
~~~
{: .bash}

> ## Assembler of Choice?
>
> Note that there generally isnt a "best assembler to use"! The choice and performance of assemblers will vary across different circumstances. Factors such as genome size, repetitiveness, GC content and others can all influence the performance of the assemblers! If one is to really do a serious genome assembly for their research/project, they should explore multiple assemblers, compare their results using a metric and decide for themselves which assembler to use! 
>
{: .warning}

> ## Check the quality of the Assembly
>
> After the initial assembly, we can get some basic assembly statistics by using the tool `assembly-stats`. It will report basic statistics about all the sequences in a fsata file e.g. N50, longest sequence, total number of nucleotides etc.
>
> ~~~
> # Change to the directories containing the "assembly.fasta" file.
> cd flye_output
> # Run assembly-stats
> assembly-stats ./assembly.fasta
> ~~~
> {: .bash}
>
> We can then see an output that looks something like this (note that you may or may not get the same result as shown, its normal!):
>
> ~~~
> stats for ./flye_output/assembly.fasta
> sum = 4532946, n = 2, ave = 2266473.00, largest = 4529393
> N50 = 4529393, n = 1
> N60 = 4529393, n = 1
> N70 = 4529393, n = 1
> N80 = 4529393, n = 1
> N90 = 4529393, n = 1
> N100 = 3553, n = 2
> N_count = 0
> Gaps = 0
> ~~~
> {: .output}
>
> In scenarios where we actually have/know the reference sequence, we can also do a quick alignment to check on the quality of the assembly! In this exercise, the "unknown strain" is actuall of NEB BL21 *E.coli*. Here we will use the tool `dnadiff` that is part of the [Mummer] package -- a fast aligner that can align complete genomes in relatively short time. `-p flye_dnadiff` defines the prefix of the dnadiff output files. `~/ngs_workshop/assembly/CP053601.1.fasta` is the reference sequence, which can be obtained from NEB and downloaded from [NCBI]. And `./assembly.fasta` is our assembly sequence which we are comparing against.
>
> ~~~
> dnadiff -p flye_dnadiff ~/ngs_workshop/assembly/CP053601.1.fasta ./assembly.fasta
> ~~~
> {: .bash}
>
> The alignment report output will be a `flye_dnadiff.report` that we can look at on a text editor.
>
{: .challenge}

### Step 4. Error Correction

After assembling our genome, we can further polish the reads to minimise potential errors in our assembly. This is typically done by remapping the trimmed and filtered raw .fastq reads back on the assembly to improve the consensus sequence generated. Once again, many programs are available for error correction, such as [racon], [minipolish], [pilon] and [medaka]. In fact, even the [flye] assembler we just used above has polishing function, which we already polished 3 times! Here we will use `medaka_consensus` to attempt to further polish to see what we can get! `-i ../R10_BL21_trimmed.fastq` points to the basecalled and filtered .fastq/fasta reads. `-d ./assembly.fasta` points to our flye assembled .fastq sequnece. `-o ./medaka_cleanup` specifies where to store the output files. `-m r1041_e82_400bps_sup_variant_v4.2.0` is the basecalling model used during sequencing.

~~~
# Change to the conda environment containing medaka
conda activate medaka

# Polish with medaka
medaka_consensus -i ../R10_BL21_trimmed.fastq -d ./assembly.fasta -o ./medaka_cleanup -m r1041_e82_400bps_sup_variant_v4.2.0
~~~
{: .bash}

> ## Check the quality of the Assembly
>
> After this we can check the quality of the polished assembly once again with `dnadiff`! 
> 
> ~~~
> cd medaka_cleanup
> dnadiff -p cleanup_dnadiff ~/ngs_workshop/assembly/CP053601.1.fasta ./consensus.fasta
> ~~~
> {: .bash}
>
> What did Medaka change? Did the assembly get better or worse?
>
> We can also try uploading both the assembled-and-polished .fasta sequence and the reference sequence onto BLAST, and see the quality of the assembly and take a look at the dot-plot!
> 
{: .challenge}


[FastQC]: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
[reported to be of relatively lower quality]: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0257521
[nanofilt]: https://github.com/wdecoster/nanofilt
[flye]: https://github.com/mikolmogorov/Flye
[canu]: https://github.com/marbl/canu
[racon]: https://github.com/isovic/racon
[minipolish]: https://github.com/rrwick/Minipolish
[pilon]: https://github.com/broadinstitute/pilon
[medaka]: https://github.com/nanoporetech/medaka
[Mummer]: https://mummer4.github.io/
[NCBI]: https://www.ncbi.nlm.nih.gov/nuccore/CP053601
