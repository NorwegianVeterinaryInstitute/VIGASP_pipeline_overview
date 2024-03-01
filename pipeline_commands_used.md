## Assembly Annotation
#### Assembly - Shovill 1.0.4 
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --namefmt contig%05d --depth 100 --minlen 0 --mincov 0 --assembler spades
```

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

```
spades.py -1 R1.fastq -2 R2.fastq --isolate --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,51,71,91,111 --threads 16 --memory 32 --tmp-dir /opt/galaxy/tmp/ --merged flash.extendedFrags.fastq.gz
```

#### spaTyper 0.3.3

## MLST
#### Assembly - Shovill 1.0.4 
#### QUAST 5.0.2
#### MLST 2.16.1

## SISTR
#### Assembly - Shovill 1.1.0     
#### SISTR - 1.1.1

## CoreGenomeSNP_Phylogeny
#### Assembly - Shovill 1.1.0
#### ParSNP - 2.0.3
#### HarvestTools - 1.2.0
#### Gubbins - 3.2.0
#### MaskGubbins 
#### IQ-TREE - 2.2.6
#### SNP Distance - 0.8.2

## Reads_QC 
#### Fastq Stats - FastQC
#### Species/contamination prediction - kraken2
#### Species abundance - bracken

