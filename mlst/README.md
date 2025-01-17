MLST
===================

This project documents MLST service


Documentation
=============

## What is it?

The MLST service contains one perl script *mlst.pl* which is the script of the lates
version of the MLST service. The method enables investigators to determine the ST based on WGS data.

## Content of the repository
1. mlst.pl      - the program
2. INSTALL_DB   - shell script for downloading the MLST database
3. UPDATE_DB    - shell script for updating the database to the newest version
4. VALIDATE_DB  - python script for verifying the database contains all
                  required files 
5. brew.sh      - shell script for installing dependencies
6. makefile     - make script for installing dependencies
7. test.fsa     - test fasta file

## Installation

Setting up MLST
```bash
# Go to wanted location for resfinder
cd /path/to/some/dir
# Clone and enter the mlst directory
git clone https://bitbucket.org/genomicepidemiology/mlst.git
cd mlst
```

Installing up the MLST database
```bash
cd /path/to/mlst
./INSTALL_DB database

# Check all DB scripts works, and validate the database is correct
./UPDATE_DB database
./VALIDATE_DB database
```

Installing dependencies:
Perlbrew is used to manage isolated perl environments. To install it run
```bash
bash brew.sh
```

This will install Perlbrew with Perl 5.10, along with CPAN minus as
package manager.
Blast will also be installed when running brew.sh if BlastAll and FormatDB are
not already installed and place in the user's path.
After running brew.sh and installing Blast add this command to the end of your
~/bash_profile to add BlastAll and FormatDB to the user's path

```bash
export PATH=$PATH:blast-2.2.26/bin
```

If you want to download the two external tools from the Blast package, BlastAll
and FormatDB, yourself go to
```url
ftp://ftp.ncbi.nlm.nih.gov/blast/executables/release/LATEST
```

and download the version for your OS with the format:
```url
blast-version-architecture-OS.tar.gz
```

after unzipping the file, add this command to the end of your ~/bash_profile.
```bash
export PATH=$PATH:/path/to/blast-folder/bin
```

where path/to/blast-folder is the folder you unzipped.

The Perl dependencies works in Perl 5.10 and is installed with CPAN minus as
package manager.
If you have choosen to install a local perl when running *brew.sh* the Perl
dependencies can be installed by the following
```bash
perlbrew use perl-5.10.0
make install
```

When running MLST you also need to do it through perlbrew
```bash
perlbrew use perl-5.10.0
```

If you are using Perl 5.10.0 you can just run MLST directly in the command-line
after the dependencies are installed with
```bash
make install
```

If another version of Perl is used the Perl modules might fail when running the script. 

The scripts are self contained. You just have to copy them to where they should
be used. Only the *database* folder needs to be updated mannually.

Remember to add the program to your system path if you want to be able to invoke the 
program without calling the full path.
If you don't do that you have to write the full path to the program when using it.

## Usage

The program can be invoked with the -h option to get help and more information of the service.

```bash
Usage: perl mlst.pl [options]

Options:

    -h HELP
                    Prints a message with options and information to the screen
    -d DATABASE
                    The path to where you have located the database folder
    -b BLAST
                    The path to the location of blast-2.2.26 if it is not added
                    to the users path (see the install guide in 'README.md')
    -i INFILE
                    Your input file which needs to be preassembled partial
                    or complete genomes in fasta format
    -o OUTFOLDER
                    The folder you want to have your output files stored.
                    If not specified the program will create a folder named
                    'Output' in which the result files will be stored.
    -s SPECIES
                    The MLST scheme you want to use. The options can be found
                    in the 'mlst_schemes' file in the 'database' folder
```

#### Example of use with the *database* folder located in the current directory and Blast added to the user's path
```perl
    perl mlst.pl -i test.fsa -o OUTFOLDER -s ecoli
```
#### Example of use with the *database* and *blast-2.2.26* folders loacted in other directories
```perl
    perl mlst.pl -d path/to/database -b path/to/blast-2.2.26 -i test.fsa \
     -o OUTFOLDER -s ecoli
```

## Web-server

A webserver implementing the methods is available at the [CGE website](http://www.genomicepidemiology.org/) and can be found here:
https://cge.cbs.dtu.dk/services/MLST/


## The Latest Version


The latest version can be found at
https://bitbucket.org/genomicepidemiology/mlst/overview

## Documentation


The documentation available as of the date of this release can be found at
https://bitbucket.org/genomicepidemiology/mlst/overview.


Citation
=======

When using the method please cite:

Multilocus Sequence Typing of Total Genome Sequenced Bacteria.
Larsen MV, Cosentino S, Rasmussen S, Friis C, Hasman H, Marvig RL,
Jelsbak L, Sicheritz-Pont�n T, Ussery DW, Aarestrup FM and Lund O.
J. Clin. Micobiol. 2012. 50(4): 1355-1361.
PMID: 22238442         doi: 10.1128/JCM.06094-11
[Epub ahead of print]


License
=======


Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
