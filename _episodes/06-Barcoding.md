---
title: "5. Barcoding and Decoding"
teaching: 90
source: md
questions:
- "How to barcode and decode samples for sequencing?"
objectives:
- "Why do we barcode samples?"
- "Understand how to barcode samples prior to sequencing"
- "Understand how to decode sequenced data for downstream processing"
---

When running Next-Generation Sequencing (NGS) platforms, we often run multiple samples simultaneously in a single sequencing run -- known as multiplexing. This can be achieved by assigning unique molecular barcodes, such as DNA barcodes to each sample, enabling their identification and separation post sequencing. This allows for increased throughput, reduced costs (per sample) and improved efficiency by allowing us to obtain more data in less time. And is a particularly useful technique in large-scale studies, where high sample numbers are analyzed. Hence, multiplexing should almost always be done for our samples unless we require the absolute maximum throuput and sequencing depth for a particular sample or scenario.

Amongst the library preperation kits offered by ONT, [some of the kits] already include barcoding in one of their steps -- such as the [Rapid Barcoding Kits], and [Native Barcoding Kits]. These kits provides barcodes designed by ONT, and are automatically recognised and demultiplexed during sequencing in real-time by the MinKNOW app -- provided the right library preperation kit has been chosen during the run-setup. 

However, MinKNOW (and other ONT's basecalling programs, such as [Guppy]) can only automatically recognise and demultiplex these barcodes designed by ONT, and are incapable of recognising other custom barcodes that users might have designed on their own. Yet depending on the workflow, relying on such ONT library preperation kits for multiplexing might not always be practical or possible. Hence in this chapter, we will introduce how we can design our own barcodes and demultiplex them without relying on these ONT programs post basecalling. 

### Background for Exercise 1

For the remainder of this workshop, we will go through two exercises that makes use of these programs and concepts that we will introduce during the workshop, so that users can better follow and try to understand. Exercise 1 will cover content running from Chapters 06-Barcoding till 08-Variant Calling. While Exercise 2 will be covered in Chapter 09-Assembly, which will cover almost everything again and also serve as a recap.

For exercise 1, we will go through an imaginary experimental scenario utilising NGS for mutant library studies. *E. coli* of undisclosed strain were transformed with a plasmid prepared with a mutant library of a particular gene of interest for the study. Due to the scale of the study, multiplexing with our own custom designed barcodes were used over the ONT's barcodes for library preperation, and sequencing was thereafter conducted on Flongle flow cells on the MINion Mk1B platform, with basecalling conducted locally in real-time on the MinKNOW app. The data used for this exercise 1 can be found in the folder *vc* from the files provided. Raw basecalled sequencing data containing 4 distinct samples are provided in *WkShop_VC.fastq*, with the list of barcodes used provided in *NP_WkShop_VC_BC_list.tsv*, and the reference wild-type gene sequence provided in *WkShop_VC_Reference.fasta*. Custom alignment was conducted with the reference wild-type gene sequence post sequencing using the `Fastq Custom Alignment` workflow in EPI2ME Agent, and the subsequent alignment files (.bam and .bai), which we will use in Chapter 08-Variant Calling are provided in the downstream folder *epi2me*.

### Barcode Generation

There are many ways to generate our own custom barcodes, 


[some of the kits]: https://store.nanoporetech.com/sample-prep.html
[Rapid Barcoding Kits]: https://store.nanoporetech.com/rapid-barcoding-sequencing-kit-96-v14.html
[Native Barcoding Kits]: https://store.nanoporetech.com/native-barcoding-kit-24-v14.html
[Guppy]: https://community.nanoporetech.com/docs/prepare/library_prep_protocols/Guppy-protocol/v/gpb_2003_v1_revax_14dec2018/guppy-software-overview
