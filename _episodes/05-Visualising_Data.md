---
title: "Visualising Processed Data"
teaching: 60
source: md
questions:
- "How to visualise data processed from EPI2ME or bash shell programs?"
objectives:
- "Methods to visualise processed data from EPI2ME and bash shell programs."
- "Understanding the processed data."
---
### SAM File


### IGV Viewer


### SAM2TSV

[SAM2TSV] is another powerful tool that we can use to visualise the alignment files, by printing the alignments as a TAB delimited file -- which we can either save as a .tsv file, or pipe into our own other codes and pipelines for downstream data analysis. It is part of JVarkit, a set of more than 100 java-based tools for bioinformatics. This package has not been included in the installation script, due to potential issues with Java versions. Here, we will first install JVarkit from the command line:

~~~
sudo apt update
# Check if java is installed:
java -version
# Install java:
sudo apt-get install default-jre
sudo apt install openjdk-17-jdk
# Actual JVARKIT installation:
cd ~
git clone "https://github.com/lindenb/jvarkit.git"
cd jvarkit
./gradlew jvarkit
~~~
{: .bash}

Thereafter, we can call the SAM2TSV tool from any directory with the format below. The following command produces an example output from a toy-example included in the JVarkit package.

~~~
#from anywhere, using the "~":
java -jar ~/jvarkit/dist/jvarkit.jar sam2tsv -R ~/jvarkit/src/test/resources/toy.fa ~/jvarkit/src/test/resources/toy.bam
~~~
{: .bash}

In the code above, `java -jar ~/jvarkit/dist/jvarkit.jar` is used to call the main JVarkit tool. The `sam2tsv` line tells the computer we specifically want to use the SAM2TSV program within the JVarkit tool packages. `-R ~/jvarkit/src/test/resources/toy.fa` points to the reference **FASTA** file, and `~/jvarkit/src/test/resources/toy.bam` points to the alignment **.bam** file. Note that the reference FASTA file also requires a `.dict` file, which although it is not indicated in the command above, is still required (though in the toy example above, it has already been included). We can generate a `.dict` file from any `.fasta` file using the line below:

~~~
# Generate .fai file first
samtools faidx Reference.fasta
# Generate .dict file, make sure the .dict file has the same name (minus the file extension) as the Reference.fasta file!
samtools dict Reference.fasta -o Reference.dict
~~~
{: .bash}

Looking at the output, we can see 10 columns of data. With each row corresponding to a single base, either coming from the Read sequence, or Reference sequence, or both. In each row, from left to right we have the:
1. `Read-Name`: Or the Read-ID of each read. Lines with the same `Read-Name` belong to the exact same strand of read (most of the time)
2. `Flag`: The SAM Flag value for the `READ-BASE` based on a given combination of properties for the read. Refer to this [Picard tool] to decode a given SAM flag value. 
3. `MAPQ`: Alignment mapping quality.
4. `CHROM`: Corresponding chromosome the read has been aligned to -- more for large e.g. human genomes
5. `READ-POS0`: The position of the base in the read DNA-sequence, with index starting from "0"
6. `READ-BASE`: The nucleotide corresponding to the position in the read DNA-sequence
7. `READ-QUAL`: The quality of the base above
8. `REF-POS1`: The position of the base in the reference sequence the corresponding `READ-BASE` has been aligned to
9. `REF-BASE`: The nucleotide corresponding to the position in the reference DNA-sequence
10. `CIGAR-OP`: The CIGAR string of the corresponding position/base in the alignment

We can then try on the file we have

### CIGAR Strings

![SAM2TSV Toy](../fig/Visualising/SAM2TSV_Toy.png)


[SAM2TSV]: https://jvarkit.readthedocs.io/en/latest/Sam2Tsv/
[Picard tool]: https://broadinstitute.github.io/picard/explain-flags.html
