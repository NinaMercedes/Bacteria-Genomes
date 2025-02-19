# Bacteria-Genomes- MRSA example
First let's download some samples from ENA for a comparative genomics approach- essentially putting whole genome sequences in a global context. Tried to match the sample sizes for each region/ country. This is a convenience sampling approach, so will not be entirely representative of global MRSA.
```
cd mrsa
# mkdir MRSA- this is where our new fastqs are located as well
cat "/mnt/storage10/nbillows/mrsa/metadata/samples_download.txt" | xargs -I {} -P 1 sh -c 'bash "/mnt/storage10/nbillows/mrsa/scripts/run_new_sample.sh" {}'
```


Let's filter our genomes using kraken. For this you will need to install the kraken2 client and kraken tools into a conda environment. Remember to change the paths and taxid in the script. 
```
conda activate kraken2
bash "/mnt/storage10/nbillows/mrsa/scripts/QC/KRAKEN2.sh"
conda deactivate
```
