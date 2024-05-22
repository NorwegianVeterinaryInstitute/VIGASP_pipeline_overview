# Here are the commands used VIGASP pipelines.
Input file names, DB locations are shortened to make the commands easy to read. 

## Assembly Annotation
#### Assembly - Shovill 1.0.4 
```
shovill --outdir out --cpus 8 --ram 4 --R1 R1.fastq --R2 R2.fastq --namefmt contig%05d --depth 100 --minlen 0 --mincov 0 --assembler spades
```

### Trimmomatic
```
trimmomatic PE -threads 8 -phred33 \/opt\/irida\/data\/sequence\/15325\/2\/240423_M06578\.Aga32_S15_R1_001\.fastq \/opt\/irida\/data\/sequence\/15326\/2\/240423_M06578\.Aga32_S15_R2_001\.fastq R1.fq.gz /dev/null R2.fq.gz /dev/null ILLUMINACLIP:/opt/galaxy/21.09/database/dependencies/_conda/envs/__shovill@1.0.4/db/trimmomatic.fa:1:30:11 LEADING:3 TRAILING:3 MINLEN:30 TOPHRED33 2>&1 | sed 's/^/[trimmomatic] /' | tee -a shovill.log
```

#### SPAdes v3.13.0
```
spades.py --pe1-1 1.fastq.gz --pe1-2 2.fastq.gz --only-assembler --threads 8 --memory 4 -o spades --tmp-dir /opt/galaxy/tmp -k 31,51,71,91,111  --pe1-m flash.extendedFrags.fastq
```

### BWA
```
bwa index spades.fasta 2>&1 | sed 's/^/[bwa-index] /' | tee -a shovill.log
```

### samtools
```
samtools faidx spades.fasta 2>&1 | sed 's/^/[faidx] /' | tee -a shovill.log
```

### BWA & samclip & samtools
```
(bwa mem -v 3 -x intractg -t 8 spades.fasta R1.fq.gz R2.fq.gz | samclip --ref spades.fasta.fai | samtools sort --threads 1 -m 2048m --reference spades.fasta -T /opt/galaxy/tmp/samtools.3228369 -o shovill.bam) 2>&1 | sed 's/^/[bwa+samtools-sort] /' | tee -a shovill.log

samtools index shovill.bam 2>&1 | sed 's/^/[samtools-index] /' | tee -a shovill.log
```

### Pilon
```
pilon --genome spades.fasta --frags shovill.bam --minmq 60 --minqual 3 --fix bases --output pilon --threads 8 --changes --mindepth 0.25 2>&1 | sed 's/^/[pilon] /' | tee -a shovill.log
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
```
quast --threads ${GALAXY_SLOTS:-4} -o outputdir  --min-contig 500 -l  '2024-01-4149-1-1-1-1' --contig-thresholds 0,1000 /opt/galaxy/21.09/database/objects/2/d/3/dataset_2d322def-402f-4570-b597-ff8a6ebed4da.dat 
```
#### MLST 2.16.1
```
ln -s 'dataset_2d322def-402f-4570-b597-ff8a6ebed4da.dat' '2024-01-4149-1-1-1-1' && touch "novel_alleles.fasta" &&  mlst --nopath --threads "${GALAXY_SLOTS:-1}" --minid=95 --mincov=10 --novel 'outputs/galaxy_dataset_a09d5441-87d4-4636-95f9-8216c33d6664.dat' --minscore=50 'Sample_ID' > "outputs/galaxy_dataset_8fff3fe0-234f-40bc-80ad-dc747955bf06.dat" && touch 'database/jobs_directory/000/114/114485/outputs/galaxy_dataset_a09d5441-87d4-4636-95f9-8216c33d6664.dat'
```

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
#### SNP_SITES
#### IQ-TREE - 2.2.6
#### SNP Distance - 0.8.2

## Reads_QC 
#### Fastq Stats - FastQC 0.73
```
ln -s 'R1_001.fastq' 'forward' && mkdir -p 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files' && fastqc --outdir 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files'   --threads ${GALAXY_SLOTS:-2} --quiet --extract  --kmers 7 -f 'fastq' 'forward'  && cp 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files'/*/fastqc_data.txt output.txt && cp 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files'/*\.html output.html

ln -s 'R2_001.fastq' 'reverse' && mkdir -p 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files' && fastqc --outdir 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files'   --threads ${GALAXY_SLOTS:-2} --quiet --extract  --kmers 7 -f 'fastq' 'reverse'  && cp 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files'/*/fastqc_data.txt output.txt && cp 'jobs_directory/096/96184/working/dataset_a0567418-d642-4cbc-9bc7-4d06337537a1_files'/*\.html output.html

```
#### Species/contamination prediction - kraken2
Kraken2 command 
```
kraken2 --threads ${GALAXY_SLOTS:-1} --db 'kraken2_databases/2022-03-14T135049Z_standard_prebuilt_8'    --paired 'R1_001.fastq' 'R2_001.fastq'   --confidence '0.0' --minimum-base-quality '0' --minimum-hit-groups '2'    --report 'galaxy_dataset_6891a190-e88b-45e5-ac1d-1f6b89a13cd9.dat'     > 'outputs/galaxy_dataset_a4e4ca28-ee73-409c-ad1a-9050eb9a6432.dat'
```
bracken command 
```
est_abundance.py -i 'dataset_6891a190-e88b-45e5-ac1d-1f6b89a13cd9.dat' -k 'kraken2_databases/2022-03-14T135049Z_standard_prebuilt_8/database150mers.kmer_distrib' -l S -t 10 -o 'outputs/galaxy_dataset_108d1f24-fd4e-47bc-9c44-d9944fa2d28a.dat'
```

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
```
python3 run_resfinder.py -ifq R1.fastq R2.fastq -s "$species_name" -o . -db_res db_resfinder/ -db_point db_pointfinder/ --acquired --point -t 0.9 -l 0.6 -t_p 0.9 -l_p 0.6
```
#### ResPointFinder EFSA_2021
#### ResFinder DB EFSA_2021
#### PointFinder DB EFSA_2021


## VirulenceFinder 
#### VirulenceFindere 2.0.4
```
python3 virulencefinder.py -i $input1.forward $input1.reverse -x -o output -p   virulencefinder_db/ --speciesinfo_json "{\"$species_name\":\"tax\"}" -t $identity -l $length
```
## SeroTypeFinder
#### SeroTypeFinder 2.0.2
DB location is stored in env variable (use "printenv" command inside the conda env to see the details). 
```
serotypefinder -x -i $infile -l 0.60 -t 0.85
```
