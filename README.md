# VIGASP_pipeline_overview

## As of Feb 2024: 
- Total number of pipelines: 12
- Number of pipelines we use which came with IRIDA: 4 (1 without modifications, 3 we needed to modify to work)

## List of Pipelines
1. Assembly and Annotation Pipeline
2. MLST Pipeline NVI - Modified by NVI
3. SISTR Pipeline v1.1.1 (NVI) - Modified by NVI
4. Species Abundance Pipeline - Modified by NVI
5. Assembly_QC Pipeline - NVI Developed 
6. Phylo-CoreGenomeSNP Pipeline - NVI Developed 
7. Reads_QC Pipeline - NVI Developed 
8. ResPointFinder - NVI Developed 
9. ResPointFinder2 (EFSA 2022) - NVI Developed  
10. SeroTypeFinder Pipeline - NVI Developed  
11. Virulence_Finder - NVI Developed 
12. spaTyper Pipeline - NVI Developed 

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

3. Species Abundance Pipeline and Reads_QC:
   - Update Kraken2 DB version to the latest (Oct 2023)
     Note:  Discuss with Thomas before  
   - Both the pipelines use Kraken2. So, most likely, we can remove the "Species Abundance Pipeline"

## New Pipelines: 
1. Kleborate - Klebsilla
2. Sequence depth (qualimap2) - Requested by Eve 

