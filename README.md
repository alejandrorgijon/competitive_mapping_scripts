# Competitive mapping
In short, the raw metagenomic reads of all metagenomes were trimmed using the Microbial Genomes Atlas v1.3.8.2 (MiGA) (1), and the competitive mapping was performed using Strobealign v0.11.0 (2).

Our pipeline was divided into 9 different steps:
- 01.Download_metagenomes.pbs: script used to download the FastQ files of the analyzed metagenomes. It leverages the script “SRA.download.bash” from the Enveomics collection (3).
- 02.Create_Miga_project_and_copy_metagenomes.pbs: script used to create a MiGA environment (“miga new”), in which the fastQ files were copied to (“miga add”).
- 03.Trimming_metagenomes.pbs: script used to trim all raw fastQ files (“miga run -r trimmed_reads”).
- 04.Calculate_trimming_statistics.pbs: script used to estimate the trimming statistics (including the number of reads, the average length of reads (bp), GC content (%), GC skew (%), etc).
- 05.Calculate_Strobealign_index.pbs: script used to compute the different strobealign indexes with different read lengths (“strobealign --create-index -r 50/100/125/150/250/300/400”). 
- 06.Mapping.pbs: script to compute the mapping (“strobealign --use-index”) by using the Strobealign indexes and the concatenated fnas.
- 07.Genome_equivalents.pbs: script used to estimate genome equivalents (total number of sequenced base pairs in the trimmed fastQ file divided by the average genome size in the metagenome) for each trimmed metagenome. This script leverages MicrobeCensus v1.1.0 (4).
- 08.Tad80.pbs: script to used to calculate the Truncated Average Depth 80%. It leverages the BedGraph.tad.rb script from the Enveomics collection (3).
- 09.Report.pbs: script used to estimate the relative abundance of each species-cluster per metagenome. 

# Reference of paper

Rodríguez-Gijón A, Milke F, Dharamshi J, Pacheco-Valenciana A, Hampel JJ, Damashek J, Wienhausen G, Rodriguez-R. LM, Garcia SL. 2024. The effect of genome size on ecological success is mediated by genomic features and biotic factors in aquatic prokaryotes. Manuscript.

# Other relevant reference

(1) Rodriguez-R LM, Gunturu S, Harvey WT, et al. 2018. The Microbial Genomes Atlas (MiGA) webserver: taxonomic and gene diversity analysis of Archaea and Bacteria at the whole genome level. Nucleic Acids Research 2;46(W1):W282–8. 

(2) Sahlin K. 2022. Strobealign: flexible seed size enables ultra-fast and accurate read alignment. Genome Biol 23(1):260. 

(3) Rodriguez-R LM, Konstantinidis KT. 2016. The enveomics collection: a toolbox for specialized analyses of microbial genomes and metagenomes. PeerJ Preprints; 2016.

(4) Nayfach S, Pollard KS. 2015Average genome size estimation improves comparative metagenomics and sheds light on the functional ecology of the human microbiome. Genome Biol 16(1):5

