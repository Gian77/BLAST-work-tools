# BLAST-work-tools

In this repo some usuefull script to interact with the BLAST program and the NCBI sequence database.

### Download the reference DB

To reporduce this you need to:<br> 

* download and extract the all the `nt`files present at https://ftp.ncbi.nlm.nih.gov/blast/db/<br>
e.g. `wget https://ftp.ncbi.nlm.nih.gov/blast/db/nt.49.tar.gz`<br>

* download and extract the`taxdb.tar.gz`<br>
* download and extract the `taxdump.tar.gz` at https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/<br>

### Install softwares

You will need to install blast and taxonkit. I personally like to use conda for this and I have an environemtn set up for working with NCBI and BLAST with the tools I need.
```
[benucci@dev-intel14 BLAST_to_NCBI]$ conda info --envs
[benucci@dev-intel14 BLAST_to_NCBI]$ conda search -c bioconda taxonkit
[benucci@dev-intel14 BLAST_to_NCBI]$ conda search -c bioconda blast
[benucci@dev-intel14 BLAST_to_NCBI]$ conda create --name blast_tools
[benucci@dev-intel14 BLAST_to_NCBI]$ conda info --envs
[benucci@dev-intel14 BLAST_to_NCBI]$ conda activate blast_tools
[benucci@dev-intel14 BLAST_to_NCBI]$ conda list
[benucci@dev-intel14 BLAST_to_NCBI]$ conda install -c bioconda blast=2.12.0=pl5262h3289130_0
[benucci@dev-intel14 BLAST_to_NCBI]$ conda search -c bioconda taxonkit
[benucci@dev-intel14 BLAST_to_NCBI]$ conda install -c bioconda taxonkit=0.9.0=h9ee0642_0
[benucci@dev-intel14 BLAST_to_NCBI]$ conda list
```
### Running the scripts

The script BlastLocal.sb is written to be run in the HPCC at Michigan State University but can be esily modified to run locally or in another type of cloud computing server.

What the script does? The script BLAST a list of sequences in `.fasta` format to the NCBI nucleotide reference DB. It saves the top 10 results of the blast and several fields `6 qseqid sseqid pident qlen length mismatch gapopen evalue bitscore qcovs sskingdom staxid ssciname staxids` specified with the `-outfmt` option that can be easilty changed. Additionally it matches the taxonomy ids and retrive the full lineage for eact BLAST hit. The output is a tab delimited file.

An example is reported below:

```
sbatch BlastLocal.sb /mnt/home/benucci/BLAST_to_NCBI/otus_Alveolata.fasta Alveolata
```

The first field is the input file, the second is the name we will add to the name of the output result file.

__NOTE__
Make sure you download all the `nt.{i}.tar.gz` files, so check the NCBI website before, then modify the scripts accordingly. For example, now we have up to `nt.87.tar.gz`, but this will grow with NCBI growth.
