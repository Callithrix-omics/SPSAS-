---
editor_options: 
  markdown: 
    wrap: 72
---

## TUTORIAL -- Consensus genome sequence inference 

This is a super short tutorial on downloading data and inferring
consensus viral genome sequences from ONT data.

It is largely based on the official ARTIC network documentation
(<https://artic.network/ncov-2019>).

First, download the sequencing data at
<https://www.dropbox.com/scl/fo/4mpf9nlbnl6ba0kj4o1gr/h?rlkey=3umc1ily051noc5g49vbdrulj&dl=0>.

Then move the files to the target directory and set it as the working
directory:

```{bash}
 $ mv /home/artic/Downloads/SPSAS.zip /home/artic/Documents/artic/
 $ cd /home/artic/Documents/artic/ 
```

Extract the files in the command line and change directory:

```{bash}
$ unzip SPSAS.zip 
$ cd SPSAS
```

Activate the conda environment and fix a dependency path:

```{bash}
$ conda activate artic-ncov2019 
$ export HDF5_PLUGIN_PATH=/usr/local/hdf5/lib/plugin 
```

Use the reads filtering routine of the artic pipeline:

(-directory fastq_pass/barcodeXX represents one of the barcode folders
barcode26 barcode28 barcode30)

```{bash}
$ artic guppyplex –min-length 400 –max-length 700 –directory fastq_pass/barcodeXX –prefix SPSAS_sequencing_data 
```

Create a directory to store the output of the next step:

```{bash}
 $ mkdir output
```

Use the consensus sequence inference routine:

```{bash}
$ artic minion –normalise 200 –threads 2 –scheme-directory /home/artic/Documents/artic/nCoV19_Manaus_Library87_20211026/primer_schemes/ –read-file /home/artic/Documents/artic/SPSAS/SPSAS_sequencing_data_.fastq –fast5-directory /home/artic/Documents/artic/SPSAS/fast5/ –sequencing-summary /home/artic/Documents/artic/nCoV19_Manaus_Library87_20211026/sequencing_summary_FAS96440_ee810178.txt nCoV-2019/V3 output/SPSAS_data 

```

Now open the file consensus sequence fasta file with aliview.

------------------------------------------------------------------------

Corrected command line


    $ cd Downloads
    $ unzip SPSAS.zip
    $ mkdir SPSAS
    $ mv fast5_pass SPSAS
    $ mv fastq_pass SPSAS
    $ conda activate artic-ncov2019 
    $ export HDF5_PLUGIN_PATH=/usr/local/hdf5/lib/plugin 
    $ cd SPSAS
    $ artic guppyplex --min-length 400 --max-length 700 --directory fastq_pass/barcode26 --prefix SPSAS_sequencing_data 

    $ mkdir output
    $ artic minion --normalise 200 --threads 2 --scheme-directory  /home/artic/Documents/artic/nCoV19_Manaus_Library87_20210126/primer_schemes --read-file /home/artic/Downloads/SPSAS/SPSAS_sequencing_data_barcode26.fastq --fast5-directory /home/artic/Documents/artic/SPSAS/fast5/ --sequencing-summary  /home/artic/Documents/artic/nCoV19_Manaus_Library87_20210126/sequencing_summary_FAS96440_ee810178.txt nCoV-2019/V3 output/SPSAS_data

    $ aliview
