@ A. Tayyrov
# Transcriptome-analysis workflow
This is genaral steps in analysing bulk RNA-seq data. It is never good idea to blindly follow any methods as these methods always requires adjustment based on a spesific needs of a project. However, these steps still should give a geeneral sense of the workflow for RNA-seq analysis.

## Step 1: Preparing your datasets.

Although small scale analysis can be done on a personal computer, we will need high-performance computing (HPC) environment for most of our analysis. THus, first connect your remote servers and setup a working folders for this project. 

#### I recommend structuring your folders as below:
``` bash
── name_of_current_project/

  │   └── genome_data/
  │          - Host genome file (.FASTA) 
  │          - Genome annotation file (.GTF/.GFF)
  │          - indexed genome files using STAR
  
  │   └── input_data/
  │          - raw RNAseq fastq files
  
  │   └── results/                   
  │       ├── initial_fastqc (multiQC)/         
  │       ├── trimmed_fastq_files/     
  │       ├── aligned_BAM_files/      
  │       ├── gene_counts/       
  │       ├── multiQC/            
  │   ...and other folders based on specific requirements of a project
  │  
```
#### Downloading files to remote servers
Download genome and fastq files into corrseponding folders using *wget*. 
If the access to the files requires login and password make sure to use wget command as below:
```
wget --user=write_your_username --ask-password url_of_file_to_be_downloaded
```
To transfer files from your local computer you can use Secure Shell (SSH) protocol's secury copy (*scp*) utility as below:
```
scp myfile.txt remoteuser@remoteserver:/remote/folder/
```
#### Checking integrity of downloaded files
Most of the time there is checksum file (.MD5) along with the sequence files
This checksum file contains a string of characters and numbers generated by running a cryptographic hash function against each individual file 
The checksum files are used to verify that a file is genuine, error free and has not been changed from it's original source.
**md5sum** can be used to calculate hash algorithm of the files and check its value aginst downloaded checksum file as below:
```
md5sum --check donwloaded_ckecksum_file   //run this command in the folder (or provide path) as downloaded files, it will give "OK" for each file if their hash string matches
```

