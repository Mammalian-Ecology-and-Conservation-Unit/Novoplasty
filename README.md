# Novoplasty
 This repository contains steps for extracting mitogenomes from whole genome data
 
 ## Pull NOVOPlasty from github
The website is here: https://github.com/ndierckx/NOVOPlasty

I cloned the repository to the bin directory: 
```
git clone https://github.com/ndierckx/NOVOPlasty.git
```

## Need to assign the seed to a reference mtDNA 

I used a complete mitogenome sequence of the same species, which I found avaliable on NCBI. 

I copied the fasta file and pasted it in: 
```
touch MitoREF.fa
```

## Make the config text file to run NOVOPlasty 

First, we need to make the config file: 
```
touch configfile.txt
```
Then we need to fill in the required information instructed by the Novoplasty manual:

```
Project name         = projectname
Insert size          = 300
Insert size aut      = yes
Read Length          = 150
Type                 = mito
Genome Range         = 12000-20000
K-mer                = 39
Insert Range         = 1.6
Insert Range strict  = 1.2
Single/Paired        = PE
Max memory           = 20
Extended log         = 1
Save assembled reads = yes
Combined reads       =
Forward reads        = /home/fastqfiles/yourfile.fastq #(your directory info would go here)
Reverse reads        = /home/fastqfiles/yourfile.fastq #(your directory info would go here)
Seed Input           = /home//projects/Novoplasty/MitoREF.fa #(your directory info would go here)
Reference            = /home//projects/Novoplasty/MitoREF.fa #(your directory info would go here)
```

## Running NOVOPlasty

Make a shell file to run on a cluster
```
test.sh
```
And here's what I placed in the shell file
```
#!/bin/bash -l
#SBATCH -t 10:00:00
#SBATCH -p med
#SBATCH --mem=8G
#SBATCH -o "test.out"

perl ~/bin/NOVOPlasty/NOVOPlasty2.7.2.pl -c ~/projects/Novoplasty/configfile.txt > ~/projects/Novoplasty/output.NOVOPlasty.log
```
To run the command on the cluster, we can do: 
```
sbatch test.sh   
```
