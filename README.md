# CnR
Pipeline to analyze CUT&amp;RUN data on the HPCC using SLURM.

## Steps
1. Create a directory for analysis.
2. Prepare a samplesheet table in csv format. (ex: samplesheet.csv)
3. Make a Nextflow config file.
4. Download the reference genome and file in your directory.
5. Write a bash script to run the pipeline using SLURM.
6. Run the pipeline from your CUT&amp;RUN directory.

## Create a directory
Login to your HPCC account using OnDemand. Navigate to your home directory by clicking 'Files' in the navigation bar. Select 'Home Directory'.

Create a directory for your analysis by clicking 'New Directory'. Name your directory (ex: cutandrun). Navigate to the newly created CUT&amp;RUN directory.

## Make a samplesheet table
In your CUT&amp;RUN directory, click 'New File'. Name the file 'samplesheet.csv'. Click the `⋮` symbol and select edit. Create the samplesheet table, for example:
```
group,replicate,fastq_1,fastq_2,control
h3k27me3,1,h3k27me3_rep1_r1.fastq.gz,h3k27me3_rep1_r2.fastq.gz,igg_ctrl
h3k27me3,2,h3k27me3_rep2_r1.fastq.gz,h3k27me3_rep2_r2.fastq.gz,igg_ctrl
igg_ctrl,1,igg_rep1_r1.fastq.gz,igg_rep1_r2.fastq.gz,
igg_ctrl,2,igg_rep2_r1.fastq.gz,igg_rep2_r2.fastq.gz,
```
Save the samplesheet.csv file and return to your CUT&amp;RUN directory.

## Make a Nextflow configuration file to use SLURM as the process executor
In your CUT&amp;RUN directory, click `New File`. Name the file 'nextflow.config'. Click the `⋮` symbol and select edit. Create the Nextflow config file:
```
process {
    executor = 'slurm'
}
```
Save the nextflow.config file and return to your CUT&amp;RUN directory.

## Download the reference genome and gtf files in your CUT&amp;RUN directory
In your CUT&amp;RUN directory, click `Open in Terminal` to enter a development node. Download the most recent genome primary assembly and gtf for the organism of interest from [Ensembl](https://ensembl.org/). This may take more than a few minutes. For example:
```
wget https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

wget https://ftp.ensembl.org/pub/release-108/gtf/homo_sapiens/Homo_sapiens.GRCh38.108.gtf.gz
```
Note: If you do not download the genome and gtf for the organism that the RNA-seq data is derived from, this pipeline will not work correctly.

## Write a bash script to run the pipeline using SLURM
In your CUT&amp;RUN directory, click `New File`. Name the file 'run_cutandrun.sb;. Write the bash script, using #SBATCH directives to set resources, for example:
```
#!/bin/bash

#SBATCH --job-name=$jobname_cutandrun
#SBATCH --time=24:00:00
#SBATCH --mem=24GB
#SBATCH --cpus-per-task=8

cd $HOME/cutandrun
module load Nextflow/23.10.0

nextflow pull nf-core/cutandrun
nextflow run nf-core/cutandrun -r 3.2.2 --input ./samplesheet.csv  -profile singularity --outdir ./cutandrun_results --fasta ./Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz --gtf ./Homo_sapiens.GRCh38.108.gtf.gz -work-dir $SCRATCH/cutandrun_work -c ./nextflow.config
```
Save the run_cutandrun.sb file and return to your CUT&amp;RUN directory.

## Run the pipeline
In your CUT&amp;RUN directory, click `Open in Terminal` to enter a development node. Run jobs on the SLURM cluster:
```
sbatch run_cutandrun.sb
```
Check the status of your pipeline job:
```
squeue -u $username
```
Note: replace $username with your username
