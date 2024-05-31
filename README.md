# SF-Coyote-Diet-Metabarcoding

**Title:** Urban landscape heterogeneity shapes individual and territory-level variation in coyote diet

**Abstract:** In the past decade, studies have demonstrated that several traits, including foraging behavior and diet, differ between urban and nonurban wildlife populations. However, little is known about how environmental heterogeneity shapes dietary variation of organisms within cities. We examined the diets of coyotes (*Canis latrans*) in San Francisco to quantify territory- and individual-level dietary differences and determine how within-city variation in land cover and land use affect coyote diet. We genotyped fecal samples for individual coyote identification and quantified diet with DNA metabarcoding. The highest contributor to coyote diet was anthropogenic food followed by small mammals. The most frequently detected species were domestic chicken, pocket gopher (*Thomomys bottae*), pig, and raccoon (*Procyon lotor*). Diet composition varied significantly across territories and among individuals. Within family groups, however, individual diets were relatively consistent. The representation of anthropogenic food in scats was correlated with impervious surface cover, suggesting that coyotes consumed more human food in more urbanized territories. The representation of invasive, human-commensal rodents in the diet was correlated with the number of food services in a territory. Overall, our results revealed substantial intraspecific variation in coyote diet associated with urban heterogeneity and point to a diversifying effect of urbanization on animal diet.

**Code version:** R v 4.2.1

**To add:**

-   Overview of folders/files and their contents

-   Instructions for users to run the software (e.g. explain the project workflow and any configuration parameters of your software)

## Code:

## 1. Sequence-Processing

-   Trimming-Reads.Rmd: trim raw fastq files with cutadapt. High performance computing required.
-   DADA2.Rmd: correct amplicon errors and infer amplicon sequence variants (ASVs) with DADA2 denoising algorithm. High performance computing required.

## 2. Assign-Taxonomy

-   BLAST.Rmd: create local BLAST database of 12SV5 sequences of vertebrate genera recovered from pilot studies. Use the *blastn* feature of BLAST+ to assign ASVs via the custom database and append or correct as needed with the nucleotide database of NCBI available online.

## 3. Filtering-and-QC

-   FilteringReads.Rmd: manually filter denoised data. The input files are ASV count tables output by DADA2 during sequence processing with taxonomy assigned by BLAST+ (output of step 1). These count tables are provided.

## 4. Data Visualization and Statistical Analyses

Creating figures or conducting statistical analyses requires that filtering and QC steps have been run as denoised and filtered data frames are required for visualizing and analyzing diet data.

### Diet-Plots

-   Generate Figures 1 and 2 in the main text to visualize relative amounts of diet items in the population diet and among biological seasons, territories, and individuals.

### Regression-Analyses

-   Correlation matrix of land cover and land use covariates (Figure S3).
-   Beta regression for RRA and a quasibinomial GLM for FOO to test the effect of percent cover of impervious surfaces on the proportion and frequency of anthropogenic food in each territory and the number of food services on the proportion and frequency of nuisance rodents in the diet in each territory.
-   R script to generate Figure 3 in the manuscript, showing correlation between land cover/land use and diet items.

### iNEXT

-   R script for generating rarefaction curve plots and calculating diversity metrics and sample coverage for coyote territories and individuals.

### nMDS

-   R script constructing dissimilarity matrices and ordinating with non-metric multidimensional scaling to visualize dietary differences among biological seasons, territories, and individuals.

### PERMANOVA

-   Permutation-based multivariate analysis of variance tests to investigate differences in diet as a function of biological season and territory as well as among individuals and family groups.

### SIMPER

-   Similarity percentage analysis to assess which diet items contributed the most to observed differences in coyote diets among territories.

### Replication-Analyses

-   Add details here
-   30 extraction replicates that were actually metabarcoded; 44 PCR replicates from mini exp 7 that intersect; 78 PCR replicates from mini exp 1 that intersect; In the end, 10+54+23 = 87 pairs remaining

### Figure for Controls

## Data Files:

### Assign-Taxonomy

-   12S_reference_lib.fasta: Custom reference library of 12SV5 sequences of all vertebrate genera recovered from pilot studies.

### Filtering-and-QC

-   batch1_reads.csv and batch2_reads.csv: ASV tables generated by DADA2 with taxonomy assigned via BLAST added.
-   All_Metadata.csv: metadata for all fecal samples
-   NoCanis_Scats.csv: list of samples names that did not generate Canis spp. reads
-   Species_FunctionalGroups.csv: categorizes diet items into functional groups

### Diet-Plots

-   12S_species_categories.csv: categorizes diet items into taxonomic groups

-   IDs.csv: lists sex and family group assignment of individual coyotes

### Regression-Analyses

-   Territory_All_Covariates.csv: land cover and land use covariates for each territory

### nMDS

-   sp.RRA.rds: model output from metaMDS RRA data
-   sp.FOO.rds: model output from metaMDS FOO data
-   sp.RRA.ind.rds: model output from metaMDS RRA data for frequently sampled coyotes
-   sp.FOO.ind.rds: model output from metaMDS FOO data for frequently sampled coyotes

### PERMANOVA

-   PERMANOVA_sample_RRA.rds: model output from 1,000 trials of RRA-based data when subsampling down to one observation per individual

-   PERMANOVA_sample_FOO.rds: model output from 1,000 trials of FOO-based data when subsampling down to one observation per individual

-   Move data files into PERMANOVA folder prior to running code
