# VIGASP_pipeline_overview

## As of Feb 2024: 
- Total number of pipelines: 12
- Number of pipelines we use which came with IRIDA: 4 (1 without modifications, 3 we needed to modify to work)

## List of Pipelines
1. Assembly and Annotation Pipeline
2. Assembly_QC Pipeline
3. MLST Pipeline NVI
4. Phylo-CoreGenomeSNP Pipeline
5. Reads_QC Pipeline
6. ResPointFinder
7. ResPointFinder2 (EFSA 2022)
8. SISTR Pipeline v1.1.1 (NVI)
9. SeroTypeFinder Pipeline
10. Species Abundance Pipeline
11. Virulence_Finder
12. spaTyper Pipeline

## Validation 
1. SeroTypeFinder:
   Draft is ready and Camilla has given her comments to finish. Jeevan has to update the document
2. SpaTyper:
   Draft is ready and Jannice has given her comments. Waiting for Marianne to send her comments to finish.
3. CoreGenomeSNP_Phylo (ALPPACA):
   Tools are updated to the latest ALPPACA version. Draft is not rady yet since we need to rerun and update the numbers. 
   

## Waiting for updates: 
1. ResPointFinder2 - End of Feb 2024
    - Update the ResPointFinder tool 
    - Update the ResFinder DB
    - Update the PointFinder DB
    - Update the DisinFinder DB

2. SeroTypeFinder - Beginning of March or earlier
   - small Change in output format to "Linelist" 

3. Species Abundance Pipeline:
   - Update Kraken2 DB version to the latest (Oct 2023)
     Note:  Discuss with Thomas before  

## New Pipelines: 
1. Kleborate - Klebsilla
2. Sequence depth (qualimap2) - Requested by Eve 

