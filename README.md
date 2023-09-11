# unmsm_practica
## Install Conda enviroment 

```bash
wget https://raw.githubusercontent.com/FranciscoAscue/unmsm_practica/main/ngs_conda.yml
```
```bash
conda env create -f ngs_conda.yml
```
## 
```bash
bwa mem -t 4 -o file.sam genome_reference.fasta file_1.fastq file_2.fastq

samtools view -b -S -o file.bam -@ 3 file.sam

samtools sort -o file_sort.bam --output-fmt BAM -@ 2 file.bam

samtools index -b -@ 2 file_sort.bam
``

