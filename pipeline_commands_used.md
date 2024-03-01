## Assembly Annotation
#### Assembly - Shovill 1.0.4 
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --namefmt contig%05d --depth 100 --minlen 0 --mincov 0 --assembler spades
```
#### SPAdes v3.13.0
```
spades.py --pe1-1 1.fastq.gz --pe1-2 2.fastq.gz --only-assembler --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,51,71,91,111  --pe1-m flash.extendedFrags.fastq
```

#### Annotation - Prokka 1.14.5
#### Assembly Quality stats - Quast 5.0.2

## Assembly_QC    
#### Assembly - Shovill 1.0.4  
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --trim --namefmt contig%05d --depth 100 --opts --threads 4 --memory 16 --tmp-dir /opt/galaxy/temp/ --minlen 0 --mincov 2 --assembler spades
```
#### SPAdes v3.13.0
```
spades.py	--pe1-1	R1.fastq	--pe1-2	R2.fastq	--only-assembler	--threads	8	--memory	4	-o	spades	--tmp-dir	/opt/galaxy/tmp	-k	31,51,71,91,111	--threads	4	--memory	16	--tmp-dir	/opt/galaxy/temp	--pe1-m	flash.extendedFrags.fastq.gz	
```
#### CheckM analyze 1.2.0
#### Quast 5.0.2
#### CheckM qa   1.2.0

## SpaTyper 
#### Assembly - Shovill 1.1.0
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --namefmt contig%05d --depth 100 --opts --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --nocorr --minlen 0 --mincov 2 --assembler spades
```
#### SPAdes genome assembler v3.15.3

```
spades.py -1 R1.fastq -2 R2.fastq --isolate --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,51,71,91,111 --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --merged flash.extendedFrags.fastq.gz
```

#### spaTyper 0.3.3

## MLST
#### Assembly - Shovill 1.0.4 
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R.fastq --trim --namefmt contig%05d --depth 100 --opts --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --minlen 1 --mincov 2 --assembler spades
```
#### SPAdes v3.13.0
```
spades.py --pe1-1 R1.fastq.gz --pe1-2 R2.fastq --only-assembler --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,55,79,103,127 --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --pe1-m flash.extendedFrags.fastq.gz
```

#### QUAST 5.0.2
#### MLST 2.16.1

## SISTR
#### Assembly - Shovill 1.1.0     
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --namefmt contig%05d --depth 100 --opts --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --minlen 1 --mincov 1 --assembler spades
```
#### SPAdes v3.15.3
```
spades.py -1 R1.fastq -2 R2.fastq --isolate --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,51,71,91,111 --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --merged flash.extendedFrags.fastq.gz
```

#### SISTR - 1.1.1

## CoreGenomeSNP_Phylogeny
#### Assembly - Shovill 1.1.0
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --namefmt contig%05d --depth 100 --opts --threads 16 --memory 64 --tmp-dir /opt/galaxy/tmp/ --nocorr --minlen 0 --mincov 2 --assembler spades
```
#### SPAdes v3.15.3
```
spades.py -1 R1.fastq.gz -2 R2.fastq.gz --isolate --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,51,71,91,111 --threads 16 --memory 64 --tmp-dir /opt/galaxy/tmp/ --merged flash.extendedFrags.fastq.gz
```

#### ParSNP - 2.0.3
#### HarvestTools - 1.2.0
#### Gubbins - 3.2.0
#### MaskGubbins 
#### IQ-TREE - 2.2.6
#### SNP Distance - 0.8.2

## Reads_QC 
#### Fastq Stats - FastQC 0.73
#### Species/contamination prediction - kraken2
#### Species abundance - bracken

## ResPointFinder3 - Updated once a year
#### ResPointFinder 4.4.2
```
python -m resfinder -o .  -s "$species_name" -l 0.6 -t 0.8 --acquired --point --disinfectant -ifq R1.fastq R2.fastq -db_res resfinder_db_2.2.1/ -db_point pointfinder_db_4.0.1/ -db_disinf disinfinder_db_2.0.1/
```  
#### ResFinder DB 2.2.1
#### PointFinder DB 4.0.1
#### DisinFinder DB 2.0.1
```
```

## ResPointFinder2
#### ResPointFinder EFSA_2022
```
python run_resfinder.py -o .  -s "$species_name" -l 0.6 -t 0.8 --acquired --point -ifq R1.fastq R2.fastq -db_res db_resfinder/ -db_point db_pointfinder/
```
#### ResFinder DB EFSA_2022
#### PointFinder DB EFSA_2022

## ResPointFinder - Updated regularly 
#### ResPointFinder EFSA_2021
#### ResFinder DB EFSA_2021
#### PointFinder DB EFSA_2021
```
```

## VirulenceFinder 
#### VirulenceFindere 2.0.4

## SeroTypeFinder
#### SeroTypeFinder 2.0.2
