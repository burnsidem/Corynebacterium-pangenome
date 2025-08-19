# corynebacterium pangenome assembly
## 1. activate the appropriate environment
the pangenome is assembled using the Anvi'o developer environment, anvio-dev.
### enter the anvio-dev environment
```sh
conda activate anvio-dev
```
## 2. reformat fasta files of each genome
```sh
anvi-script-reformat-fasta C_durumJJ1.fna -o C_durumJJ1.fa
```
the -o denotes a new output file
repeat for each genome
## 3. make a contig database for each genome
```sh
anvi-gen-contigs-database -f C_durumJJ1.fa -o C_durum_JJ1.db -n "C_durum_JJ1"
```
-f denotes 'fasta file' -n denotes the project name
repeat for each genome
## 4. run the following commands on each contig database
```sh
anvi-run-hmms -c C_durum_JJ1.db
anvi-run-ncbi-cogs -c C_durum_JJ1.db
anvi-run-kegg-kofams -c C_durum_JJ1.db
anvi-run-pfams -c C_durum_JJ1.db
```
## 5. create an external genome text file to store genomes
```sh 
nano external-genomes.txt 
```
### external genomes storage file listed in repository for reference
## 6. create a genomes storage database file
```sh
anvi-gen-genomes-storage -e external-genomes.txt -o GENOMES.db 
```
-e denotes external genomes file path
## 7. run the pangenome analysis
```sh
anvi-pan-genome -g GENOMES.db -n GENOME
```
-g denotes genomes database path 
## 8. compute genome similarity
```sh
anvi-compute-genome-similarity -e external-genomes.txt -o PAN_OUT -p PANGENOME/PANGENOME-PAN.db
```
## 9. display pangenome
```sh
anvi-display-pan -p PANGENOME/PANGENOME-PAN.db -g GENOMES.db
```
-p denotes pangenome path
### this will display an interactive pangenome in a new browser

## 10. download raw data from the genomes
```sh
anvi-summarize -p PANGENOME/PANGENOME-PAN.db -g GENOMES.db -C default
```
### this generates a .txt.gz file in the new directory, deliminated by -o
-C is the collection name, use --list-collections to show available collections

# Phylogenomic tree assembly using pangenome
We used a separate pangenome that includes the non-oral Corynebacterium, C. glutamicum. See second external genomes file for reference.

## 1. get sequences for gene clusters (single copy core genes) 
```sh
anvi-get-sequences-for-gene-clusters -g ~/tree/GENOMES.db -p Corynebacterial_Pangenome-PAN.db -o organized-pan.fa --min-num-genomes-gene-cluster-occurs 6 -max-num-genes-from-each-genome 1 --max-functional-homogeneity-index 0.9 --min-geometric-homogeneity-index 1 --concatenate-gene-cluster
```
## 2. generate phylogenomic tree 
```sh
iqtree -s organized-pan.fa -nt 6 -m WAG -bb 1000
```
## 3. display tree
```sh
anvi-interactive -p phylogenomic-profile.coryne.db --manual -t organized-pan.fa.contree
```



