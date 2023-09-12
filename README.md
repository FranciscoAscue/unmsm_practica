# unmsm_practica
## Install Conda enviroment 

```bash
wget https://raw.githubusercontent.com/FranciscoAscue/unmsm_practica/main/ngs_conda.yml
```
```bash
conda env create -f ngs_conda.yml
```
## SRA toolkit

```bash
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.0.7/sratoolkit.3.0.7-ubuntu64.tar.gz
```
## Download reference genome 

https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000146045.2/ 

```bash
curl -OJX GET "https://api.ncbi.nlm.nih.gov/datasets/v2alpha/genome/accession/GCF_000146045.2/download?include_annotation_type=GENOME_FASTA,GENOME_GFF,RNA_FASTA,CDS_FASTA,PROT_FASTA,SEQUENCE_REPORT&filename=GCF_000146045.2.zip" -H "Accept: application/zip"
```
## Alignment to reference genome

```bash
bwa mem -t 4 -o file.sam genome_reference.fasta file_1.fastq file_2.fastq

samtools view -b -S -o file.bam -@ 3 file.sam

samtools sort -o file_sort.bam --output-fmt BAM -@ 2 file.bam

samtools index -b -@ 2 file_sort.bam
```
### Separate reads from specific Chrmosome or Mitogenome 

```bash
samtools view -@ 4 -b -h file_sort.bam NC_001224.1 > mito.bam
```
#### optional transforms to fastq files
url : https://broadinstitute.github.io/picard/explain-flags.html 

```bash
samtools fastq -f 2 -1 mapped_1.fq -2 mapped_2.fq file_sort.bam
samtools fastq -f 8 -1 unmapped_1.fq -2 unmapped_2.fq file_sort.bam
```
### Consensus fasta from bam file 

```bash
samtools mpileup -A -d 0 -Q 0 mito.bam | ivar consensus -p mito -q 10 -t 0.6 -n N -m 20
```

## Online annotation of mitogenome

https://chlorobox.mpimp-golm.mpg.de/geseq.html

http://mitos.bioinf.uni-leipzig.de/index.py 


