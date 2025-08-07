# corynebacterium pangenome assembly
## 1. activate appropriate environment
the pangenome is assembled using the Anvi'o developer environment, anvio-dev.
### enter the anvio-dev environment
```sh
conda activate anvio-dev
```
## 2. reformat fasta files of each genome
```sh
anvi-script-reformat-fasta cdurumjj1.fna -o cdurumjj1.fa
```
### repeat for each genome
## 3. make a contig database for each genome
```sh
anvi-gen-contigs-database -f cdurumjj1.fa -o cdurumjj1_contigs2.db -n "cdurumjj1"
```
### repeat for each genome
## 4. create an external genome text file to store genomes
```sh 
nano external-genomes-corynebacterium.txt 
```
### external genomes storage file listed in repository for reference
## 5. create a genomes storage database file
```sh
anvi-gen-genomes-storage -e external-genomes-corynebacterium.txt -o corynebacterium-GENOMES.db 
```
## 6. run the pangenome analysis
```sh
anvi-pan-genome -g corynebacterium-GENOMES.db -n CORYNEBACTERIUM-GENOME
```
## 7. display pangenome
```sh
anvi-display-pan -p CORYNEBACTERIUM-PANGENOME/CORYNEBACTERIUM-PANGENOME-PAN.db -g corynebacterium-GENOMES.db
```
### this will display an interactive pangenome in a new browser
## 8. download raw data from the genomes
```sh
anvi-summarize -p CORYNEBACTERIUM-PANGENOME/CORYNEBACTERIUM-PANGENOME-PAN.db -g corynebacterium-GENOMES.db
```
### this generates a .txt.gz file in the new directory, deliminated by -o
## 9. export the .txt.gz file to a text file
```sh
gunzip CORYNEBACTERIUM-PANGENOME_gene_clusters_summary.txt.gz
```
### view file in excel.


