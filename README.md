# Bacteria-Genomes- MRSA example
Some old school bash scripting to support development of the new bacteria pipeline. Scripts are hard coded and need to have command line arguments added in. 
## Download samples
First let's download some samples from ENA for a comparative genomics approach- essentially putting whole genome sequences in a global context. Tried to match the sample sizes for each region/ country. This is a convenience sampling approach, so will not be entirely representative of global MRSA.
```
cd mrsa
# mkdir MRSA- this is where our new fastqs are located as well
cat "/mnt/storage10/nbillows/mrsa/metadata/samples_download.txt" | xargs -I {} -P 1 sh -c 'bash "/mnt/storage10/nbillows/mrsa/scripts/run_new_sample.sh" {}'
```
## FASTQC and Trimming
Next let's perform fastqc for each sample and trim the fastqs before any downstream processing. This will create a new directory where the QC results are stored (MRSA/qc_results). Using the fastq2matrix conda environment with additional installation of fastqc.
```
conda activate f2m
bash "/mnt/storage10/nbillows/mrsa/scripts/QC/fastqc.sh"
conda deactivate
```
## Kraken Filtering

Let's filter our trimmed fastqs using kraken. For this you will need to install the kraken2 client and kraken tools into a conda environment. Remember to change the paths and taxa_id in the script. 
```
conda activate kraken2
bash "/mnt/storage10/nbillows/mrsa/scripts/QC/KRAKEN2.sh"
conda deactivate
```


