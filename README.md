# BLAST-work-tools

In this repo some usuefull script to interact with the BLAST program and the NCBI sequence database.

### Download the reference DB

To reporduce this you need to download the NCBI nucleaotide database at this links below. This is also necessary for genome/metagenome work so you want to have a local copy in your computer or HPCC server.<br>

https://ftp.ncbi.nlm.nih.gov/blast/db/nt

you will also need the taxdb that contain `names.dmp` and `nodes.dmp`
for reconstructing taxonomies from taxonomy indexes.<br>

https://ftp.ncbi.nlm.nih.gov/blast/db/taxdb.tar.gz <br>
https://ftp.ncbi.nlm.nih.gov/blast/db/nt.49.tar.gz <br>

You also have `.md5` files in case you want to double check for dowloading erros.<br>

https://ftp.ncbi.nlm.nih.gov/blast/db/nt.49.tar.gz.md5 <br>

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

The script BlastLocal.sb is writtent o be run in the HPCC at Michigan State University but can be esily modified to run locally or in another type of cloud computing server.

What the script does? The script BLAST a list of sequences in `.fasta` format to the NCBI nucleotide reference DB. It saves the top 10 results of the blast and several fields `6 qseqid sseqid pident qlen length mismatch gapopen evalue bitscore qcovs sskingdom staxid ssciname staxids` specified with the `-outfmt` option that can be easilty changed. Additionally it matches the taxonomy ids and retrive the full lineage for eact BLAST hit. The output is a tab delimited file.

An example is reported below:

```
sbatch BlastLocal.sb /mnt/home/benucci/BLAST_to_NCBI/otus_Alveolata.fasta Alveolata
```

The first field is the input file, the second is the name we will add to the name of the output result file.
