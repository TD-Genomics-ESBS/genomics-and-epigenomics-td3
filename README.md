# Genomics and Epigenomics TD3

## De novo assembly

Si vous n'êtes pas à l'aise avec l'utilisation de la ligne de commande (CLI), vous pouvez faire le [tutoriel]() avant de commander ce TD.

Pour la partie pratique avec la CLI, une aide pour les commandes Unix est disponible [ici](). Un fichier contenant toutes les commandes utilisées dans ce TD est disponible [ici](script.sh).

### NCBI Genome database

Different strains of *Saccharomyces cerevisiae* were sequenced under the project 1011 yeast genomes, including strain SJ1L04 (Illumina HiSeq2500, paired reads, 250X coverage).

The mitochondrial genome of S. cerevisiae exhibits a greater variability (intergenic regions +presence/absence of intron) than the nuclear genome.

> [!FAQ] Which strategy seems the most suitable for comparing a strain to the reference genome in the case of the nuclear genome and in the case of the mitochondrial genome?

In the NCBI Genome database, search for the reference genome of S. cerevisiae and for the corresponding mitochondrial genome annotation (NC_001224).

> :question: What is the size of the mitochondrial genome?

> :question: The nuclear genome having a size of 12 Mb, how many paired reads were generated to obtain a sequencing depth of 250X? How could we reduce the number of reads to be processed to assemble the mitochondrial genome of this strain? Assume that the average read length is 100 (so 200 for 2 paired reads).

### Connection to server

Pour cette partie, vous allez travailler sur les serveurs du LBGI. Pour vous connecter, utilisez la commande suivante:
```
ssh -X <your_login>@tp.lbgi.fr
```

Create a working directory for this practical session and go to this directory (by example, you can call it *TDdenovo*). Copy into your directory the reads. Reads are available: `/data/TDdenovo/readsSJ1L04_*gz`

### Reads

You can view the first 12 lines of each file:
```
zcat <file_name>.gz | head –n 12
```

You can also count the lines of one of these files:
```
zcat <file_name>.gz | wc -l
```

Each file contains 4,764,652 lines.

> :question: What is the format of these files?

> :question: Is the length of the reads uniform? What can we assume?

> :question: How many reads are available?

Il y a plusieurs manières de compter le nombre de reads. 
- Compter le nombre de ligne dans le fichier, puis divisez par le nombre de ligne nécessaire pour décrire une read (un read = ? lines).

> :answer: 4,764,652 / 4 = 1,191,163 reads

### Quality of reads


Create the FastQCReport directory and run the fastqc program:

```fastqc -o FastQCReport readsSJ1L04*.fq.gz 
```

The FASTQC's results are stored in the FastQCReport directory. To view
You can view results:
cd FastQCReport
firefox readsSJ1L04_1_fastqc.html &
