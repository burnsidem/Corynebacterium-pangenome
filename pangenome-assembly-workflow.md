# corynebacterium pangenome assembly
## environment
the pangenome is assembled using the Anvi'o developer environment, anvio-dev.
enter the anvio-dev environment
```sh
conda activate anvio-dev
```
## reformat fasta files of each genome
```sh
anvi-script-reformat-fasta cdurumjj1.fna -o cdurumjj1.fa
```
repeat for each genome
## make a contig database for each genome
```sh
anvi-gen-contigs-database -f cdurumjj1.fa -o cdurumjj1_contigs2.db -n "cdurumjj1"
```
repeat for each genome
## create an external genome text file to store genomes
```sh 
nano external-genomes-corynebacterium.txt 
```
### external genomes storage file organized as followed, deliminated by tabs:
name    contigs_db_path
Corynebacterium_durum_JJ1       CdurumJJ1_contigs2.db
Corynebacterium_durum   Cdurum_contigs2.db
Corynebacterium_argentoratense  Cargentoratense_contigs2.db
Corynebacterium_matruchotii_1   Cmatruchotii1_contigs2.db
Corynebacterium_matruchotii_2   Cmatruchotii2_contigs2.db
## create a genomes storage database file
```sh
anvi-gen-genomes-storage -e external-genomes-corynebacterium.txt -o corynebacterium-GENOMES.db 
```
## run the pangenome analysis
```sh
anvi-pan-genome -g corynebacterium-GENOMES.db -n CORYNEBACTERIUM-GENOME
```
## display pangenome
```sh
anvi-display-pan -p CORYNEBACTERIUM-PANGENOME/CORYNEBACTERIUM-PANGENOME-PAN.db -g corynebacterium-GENOMES.db
```
### this will display an interactive pangenome in a new browser
## to download raw data from the genomes, use anvi-summarize
```sh
anvi-summarize -p CORYNEBACTERIUM-PANGENOME/CORYNEBACTERIUM-PANGENOME-PAN.db -g corynebacterium-GENOMES.db
```
### this generates a .txt.gz file in the new directory, deliminated by -o
## export the .txt.gz file to a text file
```sh
gunzip CORYNEBACTERIUM-PANGENOME_gene_clusters_summary.txt.gz
```
view file in excel.

