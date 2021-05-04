# update_annovar_db
scripts to automatically update ANNOVAR db


## Update ClinVar

If you wish to update (clinvar data)[https://www.ncbi.nlm.nih.gov/clinvar/] for (ANNOVAR)[https://annovar.openbioinformatics.org/en/latest/] more frequently than the ANNOVAR releases, you can use this script (works on clinvar VCF format as of May 2021).

## Requirements

- a decently recent version of (ANNOVAR)[https://annovar.openbioinformatics.org/en/latest/] (tested on 2020Jun08).


## Install

### Using conda

Clone the repo then run:

`conda env create -f environment.yml`

to create the environment and install the requirements. Then you should activate the environment:

`conda activate update_annovar_db`

## Test


To test the avinput to annovar db format conversion run:

`python avinput2annovardb.py`

this will try to convert the clinvar/GRCh37/clinvar_test.avinput to a new file linvar/GRCh37/clinvar_test.txt compatible wth ANNOVAR db format. I f you are happy woth this, then you can try the entire script.

## Usage

### Required arguments

- -d, --database-type: the database type (e.g. 'clinvar')
- -a, --annovar-path: path to ANNOVAR perl scripts folder
- -h), --humandb-path to ANNOVAR humandb/ folder (-hp)

### Optional arguments

- -g, --genome-version: genome version [GRCh37|GRCh38], default GRCh37
- -r, --rename: rename the date part of the file, e.g. clinvar_20210501.txt to clinvar_latest.txt, e.g. 'latest'

## Example

`python update_resources.py -c -hp /RS_IURC/data/MobiDL/Datasets/annovar/humandb -a /RS_IURC/data/MobiDL/Datasets/annovar/2020Jun08 -g GRCh38`

The script checks the clinvar/{genome_version}/ folder to detect a previous version of Clinvar. Then it downloads the most recent md5 file of clinvar and compares it to the version present in the clinvar/{genome_version} folder (or to nothing of there's no previous version). If the 2 md5 do not match, the script downloads the latest clinvar VCF then converts it in several steps into ANNOVAR db format.
