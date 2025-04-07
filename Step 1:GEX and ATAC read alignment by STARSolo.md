# Step 1:GEX and ATAC Read Mapping by STARSolo #
The data to be analyzed is ```PBMC from a Healthy Donor - Granulocytes Removed Through Cell Sorting (3k)``` and is available to download from https://www.10xgenomics.com/datasets/pbmc-from-a-healthy-donor-granulocytes-removed-through-cell-sorting-3-k-1-standard-1-0-0 (sign is required.)
All needed at this point is just a fastq sequence file(still 22GB) and after downloading the fastq file, ```untar``` it.  There are two direactoris, ```GEX``` and ```ATAC```.  ```GEX``` should contain 4 gzip compressed fastq files while ```ATAC``` has 12 files.  
A set of scripts below is an example scripts of STARSolo for GEX followed by ATAC.
```
GEX:

#!/opt/homebrew/bin/zsh

index=/Volumes/MySlateDrive/star_genome_index/index_human_10x
whitelist=/Volumes/MySlateDrive/10X_Whitelist/737K-arc-v1.txt
r1=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/gex/pbmc_granulocyte_sorted_3k_S1_L003_R1_001.fastq.gz
r2=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/gex/pbmc_granulocyte_sorted_3k_S1_L003_R2_001.fastq.gz
r3=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/gex/pbmc_granulocyte_sorted_3k_S1_L004_R1_001.fastq.gz
r4=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/gex/pbmc_granulocyte_sorted_3k_S1_L004_R2_001.fastq.gz

STAR --genomeDir $index \
--runThreadN 40 \
--readFilesCommand 'gzip -c -d' \
--readFilesIn $r2,$r4 $r1,$r3 \
--soloCBwhitelist $whitelist \
--soloType CB_UMI_Simple \
--soloCBstart 1 \
--soloCBlen 16 \
--soloUMIstart 17 \
--soloUMIlen 12 \
--soloStrand Forward \
--soloBarcodeReadLength 0 \
--soloBarcodeMate 0 \
--clipAdapterType CellRanger4 \
--twopassMode Basic \
--soloMultiMappers EM \
--soloFeatures Gene GeneFull Velocyto \
--outFilterMultimapNmax 10 \
--outFilterScoreMin 30 \
--soloCBmatchWLtype 1MM_multi_Nbase_pseudocounts \
--soloUMIfiltering MultiGeneUMI_CR \
--soloUMIdedup 1MM_CR \
--soloCellFilter  EmptyDrops_CR 5000 0.99 10 45000 90000  500  0.01  20000  0.01  10000 \
--soloCellReadStats Standard \
--outReadsUnmapped Fastx \
--outFileNamePrefix /Volumes/MySlateDrive/pbmc3Ksorted.GEX2 \
--outSAMtype None 

ATAC:

#!/opt/homebrew/bin/zsh

genomedir=/Volumes/MySlateDrive/star_genome_index/index_human_Gencode_GRCh38_p13
tempdir=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac
r1=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L001_R1_001.fastq.gz
r2=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L001_R2_001.fastq.gz
r3=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L001_R3_001.fastq.gz
r4=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L002_R1_001.fastq.gz
r5=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L002_R2_001.fastq.gz
r6=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L002_R3_001.fastq.gz
r7=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L003_R1_001.fastq.gz
r8=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L003_R2_001.fastq.gz
r9=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L003_R3_001.fastq.gz
r10=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L004_R1_001.fastq.gz
r11=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L004_R2_001.fastq.gz
r12=/Volumes/MySlateDrive/pbmc_granulocyte_sorted_3k/atac/pbmc_granulocyte_sorted_3k_S12_L004_R3_001.fastq.gz
whitelist=/Volumes/MySlateDrive/10X_Whitelist/737K-arc-v1.txt
out=/Volumes/MySlateDrive/atac_Solo

STAR  \
        --genomeDir $genomedir \
        --readFilesCommand 'gzip -c -d' \
        --runMode alignReads \
        --runThreadN 40 \
        --readFilesIn $r1,$r4,$r7,$r10 $r3,$r6,$r9,$r12 $r2,$r5,$r8,$r11\
        --soloType CB_samTagOut \
        --soloCBwhitelist $whitelist \
        --soloBarcodeReadLength 0 \
        --sjdbGTFfeatureExon exon \
        --soloCBmatchWLtype 1MM \
        --soloStrand Forward \
        --outSAMattributes NH HI CR CB CY UR UY sM\
        --outSAMtype BAM Unsorted \
        --outReadsUnmapped Fastx \
        --outFileNamePrefix $out
```

