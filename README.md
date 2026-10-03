# Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag


This repository is associated with the study [Francisco *et al.* preprint](https://www.biorxiv.org/content/), titled *Rapid evolutionary responses to contemporary climate change in maritime pine (Pinus pinaster Ait.) despite widespread adaptive lag*, to be submitted.  

Genomic data for the 82 range-wide *Pinus pinaster* populations from Olsson *et al.* (2025) and Francisco *et al.* (2026) is available at [Zenodo](https://zenodo.org/records/14950394). Genomic data for the two extensively sampled populations, Lacanau and Tocchi, from data paper WP3 is available at [Zenodo](https://zenodo.org/records/17054530).  

Climate change is profoundly affecting species worldwide and poses a major threat to their long-term persistence. Although trees may have the potential for rapid adaptation to changing climates, empirical evidence remains limited, and whether these long-lived organisms can adapt quickly enough to keep pace with ongoing climate change is still an open question. We combined genomic data from 82 range-wide populations of the widespread tree *Pinus pinaster* Ait. with intensive sampling of two successive cohorts from two natural populations to investigate real-time responses to contemporary climate change. Using an original genotype-environment association (GEA) approach to quantify climate (mal)adaptation, we found that most individuals from both target populations showed evidence of an adaptive lag to current climatic conditions and are predicted to face substantial maladaptation risk under future climates. Importantly, changes in genomic composition at climate-associated loci between cohorts were consistent with rapid evolutionary responses to ongoing climate change and could not be explained by neutral demographic processes alone, as supported by forward-time genetic simulations. We also observed lower realised genetic load in the younger cohort, suggesting that the dynamics of deleterious mutations may change with climatic pressure. Our work provides evidence suggesting genetic responses to contemporary climate change within a single generation, including signals of rapid evolutionary changes in genomic composition at climate-associated loci and signatures of purifying selection, despite widespread adaptive lag to current climates. These findings challenge the view that trees respond only slowly to environmental change and highlight the need to integrate evolutionary dynamics into predictive models of species persistence under future climates.

# Scripts

This repository is divided into three sections.  

The first section reuses scripts from this [repository](https://github.com/Thomas-Francisco/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/tree/main) to perform analyses related to genetic data filtering, population genetic structure, climate data extraction, and genotype-environment association (GEA) analyses aimed at identifying climate-associated genetic markers. To avoid redundancy, the original scripts are not reproduced in this repository. However, any modifications or deviations from the published workflow are documented at each step.

The second section contains analyses of genetic diversity, extraction of historical climate data from the Mid-Holocene period (approximately 6,000 years ago), estimation of Wright's neighbourhood size (Nb) using SPAGeDi, and redundancy analyses (RDA) to investigate within-population variation in climate adaptation and evolutionary responses to contemporary climate change. This section also includes the simulation framework developed to support the last analysis. 

All the scripts associated with the HTML presented below are available in the folder [Scripts](https://github.com/Thomas-Francisco/Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag/tree/main/Scripts)

The third section reuses the deleteriousness scores assigned to each mutation in [Francisco *et al.* (2026)](https://github.com/Thomas-Francisco/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/tree/main) to estimate genetic load. The scripts and HTML used to calculate these load are provided in this repository.

## Section one: Genetic filtering, population genetic structure, and genotype-environment associations (GEA) to identify climate-associated loci

### Formatting genomic and climatic data for the range-wide populations excluding the Lacanau and Tocchi populations

Genomic and climatic data were formatted to perform population genetic structure analyses and genomic analyses to identify climate-associated SNPs.

#### [Genetic_filtering](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/01_Genetic_filtering_example.html)

- Filtering genomic data for **population structure analyses** and **GEA outlier identification analyses**
mputation of missing genotypes in the second genomic dataset using the most common genotype within each gene pool, as defined by a STRUCTURE analysis with K = 10

#### [Climatic data selection](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/02_Climatic_data_example.html)

- Extraction of climatic data from coordinates for populations at 30 arc-seconds using the Climate Downscaling tool (ClimateDT, [Marchi *et al.* 2024](https://doi.org/10.3390/environments11040082)).
- Visualisation of the climatic variation across populations
- Identification of the main climatic drivers in our dataset by : pre-selecting the climatic variables, identifying the most important variables to explain the genomic variation using OrdiR2step, removing over-collinear variables and calculating the variance inflation factor (VIF)
- Calculation of the present and future (corresponding to the mean values from five global climate models (GCMs) under the socio-economic pathway 3-7.0 for the 2041-2070 period) climatic data

#### [Population genetic structure](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/03_Population_structure_example.html)

- Principal component analyses at the individual and population levels
- Graphical representation 

### Identification of climate-associated SNPs

#### [Redundancy analyses (RDA) candidate detection](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/04_Redundancy_analyses_candidate_detection_example.html)

- Identification of candidate loci using the linear RDA method not correcting for population structure
- Identification of candidate loci using the pRDA method correcting for population genetic structure using the first two axes of a PCA.
- Dectection of outliers using the Mahalanobis distance method
- **FDR 5%** threshold
- Graphical visualisation

#### [Latent factor mixed models (LFMM) candidate detection](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/05_LFMM_candidate_detection_example.html)

- Identification of candidate loci using the multivariate approach developped in LFMM2 ([Caye *et al.* 2019](https://doi.org/10.1093/molbev/msz008))
- Two latent factors were used to account for population genetic structure
- **FDR 5%** threshold
- Graphical visualisation

#### [BayPass candidate detection](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/06_BAYPASS_candidate_detection_example.html)

- Method developped by Mathieu Gautier (2015)
- Core model used to construct the Omega matrix to account for population genetic structure
- Standard covariate model (STD) used to calculate the association between SNPs and climatic predictors
- Five independent runs
- Bayes factor (BF) > 10 was used as threshold
- Graphical visualisation

#### [Gradient forest (GF) candidate detection](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/07_Gradient_forest_candidate_detection_example.html)

- Non- linear machine learning algorithm used as a GEA method by [Fitzpatrick *et al.* (2021)](https://doi.org/10.1111/1755-0998.13374)
- GF-raw not accounting for population genetic structure
- GF-corrected accounting for population genetic structure using the LFMM-corrected matrix with two latent factors
- Five independent runs
- The top 1% of the overlapping SNPs across runs with the highest association with climatic predictors was used as threshold

#### [Outlier selection](https://thomas-francisco.github.io/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/HTML/08_Outlier_selection_example.html)

- All the SNPs identified by the GEA methods presented above have been retained for subsequent analysis on climate (mal)adaptation.
  
# Section two: Genetic diversity, historical climate, Wright neighbourhood size and Redundancy analysis (RDA) to investigate within-population variability in climate adaptation and evolutionary responses to contemporary climatic changes, along with associated simulation framework. 

Analyses were performed on the Lacanau and Tocchi populations only except for the RDA analyses were the model was built with the 82 range-wide populations (see Main text of the study)

#### [1. Genetic diversity calculation across Lacanau and Tocchi populations](https://thomas-francisco.github.io/Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag/HTML/1_Genetic_diversity_Ppinaster_study.html)

- Observed heterozygosity (Hᵢ) as a measure of genetic diversity
- Calculations performed under different thresholds of minor allele count (MAC) and missing data
- Statistical comparisons of values between the Lacanau and Tocchi populations, as well as among cohorts within populations, using one-way Welch ANOVA with associated Post-hoc pairwise comparisons using Games-Howell’s tests, along with associated *p*-values

#### [2. Spatial genetic structure analysis (SGS) and Wright neighbourhood size (*Nb*) estimation](https://thomas-francisco.github.io/Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag/HTML/2_SPAGeDi_format_Ppinaster_study.html)

- Pre-processing of genomic data for analysis in SPAGeDi to assess spatial genetic structure (SGS) and estimate neighbourhood size (Nb)
- Generation of 10 replicate datasets per population (Lacanau and Tocchi)
- Description of the SPAGeDi analyses performed

#### [3. Historical climate during the Mid-Holocene period (~6,000 years ago)](https://thomas-francisco.github.io/Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag/HTML/3_Historical_climate_Ppinaster_study.html)

- Extraction of climatic data for the Lacanau and Tocchi populations based on geographic coordinates, at a spatial resolution of 30 arc-seconds from the WorldClim 1.4 database, across five global climate models (GCMs)
- Calculation of bioclimatic variables and the summer heat-moisture index (SHM) using the *biovars* R package

#### [4. Within-population variability in climate adaptation and evolutionary potential](https://thomas-francisco.github.io/Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag/HTML/4_RDA_model_within-population_and_evolutionary_responses_Ppinaster_study.html)

- Calculation of the RDA-based GEA model using the 82 range-wide populations (excluding Lacanau and Tocchi) using the climate-associated SNPs identified previously and the climatic variables for the 1901–1950 period
- Estimation of the optimal genomic composition at climate-associated loci for historical, present, and future periods in the environments of Lacanau and Tocchi using the RDA-based GEA model
- Genetic filtering followed by transformation of allele frequencies at climate-associated loci into RDA scores for each individual from Lacanau and Tocchi
- Graphical visualisation of Lacanau and Tocchi individuals in the RDA GEA space, compared both to the populations used to build the model and to the predicted optima genomic compositions
- Statistical comparison of RDA scores among within-population cohorts using two-sample *t*-tests, interpreted in relation to the predicted optima

####  5. Neutral simulation using SLiM software

- Simulation of the genotypes evolving under a neutral evolutionary scenario
- Varying initial parameters regarding pollen and seed dispersal across Lacanau and Tocchi based on observed data
- 1,000 generations
- Sampling of 500 adult and 250 juvenile individuals

# Section three: Genetic loads computation

Analyses related to the computation of the genetic load using the SnpEff and PROVEAN software were not performed in R and can be accessed in the folder [Scripts_Genetic_load](https://github.com/Thomas-Francisco/Demographic-history-shapes-forest-tree-vulnerability-to-climate-change/tree/main/Scripts_Genetic_load). First, SNPs were mapped onto the *Pinus tabuliformis* reference genome [Niu *et al.* 2022](https://www.sciencedirect.com/science/article/pii/S0092867421014288). SnpEff software (version 5.1 ) was then used to identify SNPs causing amino acid changes in protein-coding sequences [Cingolani *et al.* 2012](https://doi.org/10.4161/fly.19695). Finally, the functional impact of mutations was predicted using PROVEAN (version 1.1.5), a software that assesses the impact of mutations by evaluating sequence conservation and alignment scores across homologous proteins [Choi & Chan 2015](https://doi.org/10.1093/bioinformatics/btv195). For each SNP, PROVEAN predicted its impact on the biological function of the corresponding protein and assigned a ‘deleteriousness’ score. Mutations were considered deleterious when the PROVEAN score was lower than -2.5.
Potential and realised genetic loads were then computed using this SNP annotation in R, along with graphical visualisation and populations and cohorts comparisons. 

#### [6. Genetic load](https://thomas-francisco.github.io/Rapid-evolutionary-responses-to-contemporary-climate-change-in-Pinus-pinaster-despite-adaptive-lag/HTML/6_Genetic_load_Ppinaster_study.html)

- Computation of potential and realised genetic load
- Graphical visualisation of results
- Statistical comparisons using Games-Howell’s post hoc tests for group differences, as well as pairwise population comparisons using two-sample *t*-tests

Session info: R 4.3.2 and SLiM 5.0

