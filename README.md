This project contains the framework of the circular RNA toolbox ``circtools``.

# Installation

This package is written in python3 (3.4). It has a number of external dependencies, mostly standard bioinformatics tools:

* [bedtools (>= 2.26.0)](http://bedtools.readthedocs.io/en/latest/content/installation.html) [RBP enrichment module]
* R (>= 3.4) [Primer design module]
* [OligoArrayAux](http://unafold.rna.albany.edu/?q=DINAMelt/OligoArrayAux) 
  [required by DECIPHER Bioconductor package for annealing efficiency estimations]

Installation is managed through `python3 setup.py install`. No sudo access is required if the installation is executed with ``--user`` which will install the package in a user-writeable folder. The binaries should be installed to ``/home/$user/.local/bin/`` in case of Debian-based systems.

``Circtools`` was developed and tested on Debian and Ubuntu. 

The installation requires running python on the command line:

```
git clone git@github.com:dieterich-lab/circtools.git
cd circtools
python3 setup.py install --verbose --user
```

The installation procedure will automatically install two dependencies: [DCC](https://github.com/dieterich-lab/DCC) and [FUCHS](https://github.com/dieterich-lab/FUCHS). The primer-design module requires a working installation of [R](https://cran.r-project.org/) with [BioConductor](https://www.bioconductor.org/install/) 



# Example


# Usage

Circtools currently offers four modules:

 
```
$ circtools
usage: circtools [-V] <command> [<args>]
            Available commands:

               enrich       circular RNA RBP enrichment scan
               primer       circular RNA primer design tool
               detect       circular RNA detection with DCC
               reconstruct  circular RNA reconstruction with FUCHS
```

### detect

The ``detect`` command is an interface to [DCC](https://github.com/dieterich-lab/DCC), also developed at the Dieterich lab. Please see the corresponding [manual](https://github.com/dieterich-lab/DCC) on the GitHub project for instructions how to run DCC.
 
### reconstruct

The ``reconstruct`` command is an interface to [FUCHS](https://github.com/dieterich-lab/FUCHS). FUCHS is employing DCC-generated data to reconstruct circRNA structures. Please see the corresponding [manual](https://github.com/dieterich-lab/FUCHS) on the GitHub project for instructions how to run FUCHS.

### primer

The ``primer`` command is used to design and visualize primers required for follow up wet lab experiments to verify circRNA candidates. The full documentation for the ``primer`` module is located in its own [manual](R/circtools/vignettes/plot-transcripts.md). 

### enrich

The ``enrichment`` module may be used to identify circRNAs enriched for specific RNA binding proteins (RBP) based on DCC-identified circRNAs and processed [eCLIP](http://www.nature.com/nmeth/journal/v13/n6/full/nmeth.3810.html) data. For K526 and HepG2 cell lines plenty of this data is available through the [ENCODE](https://www.encodeproject.org/search/?type=Experiment&assay_title=eCLIP)
 project. 

```
circtools enrich --help
usage: circtools [-h] -c CIRC_RNA_INPUT -b BED_INPUT -a ANNOTATION -g
                 GENOME_FILE [-o OUTPUT_DIRECTORY] [-i NUM_ITERATIONS]
                 [-p NUM_PROCESSES] [-t TMP_DIRECTORY] [-T THRESHOLD]
                 [-P PVAL] [-H HAS_HEADER] [-F OUTPUT_FILENAME]

circular RNA RBP enrichment tools

optional arguments:
  -h, --help            show this help message and exit

Required options:
  -c CIRC_RNA_INPUT, --circ-file CIRC_RNA_INPUT
                        Path to the CircRNACount file generated by DCC
  -b BED_INPUT, --bed-input BED_INPUT
                        One or more BED files containing features to overlap
  -a ANNOTATION, --annotation ANNOTATION
                        Genome reference annotation file used to not shuffle
                        into intragenic regions
  -g GENOME_FILE, --genome GENOME_FILE
                        Genome file for use with bedtools shuffle. See
                        bedtools man page for details.

Additional options:
  -o OUTPUT_DIRECTORY, --output OUTPUT_DIRECTORY
                        The output folder for files created by circtools
                        [default: .]
  -i NUM_ITERATIONS, --iterations NUM_ITERATIONS
                        Number of iterations for CLIP shuffling [default:
                        1000]
  -p NUM_PROCESSES, --processes NUM_PROCESSES
                        Number of threads to distribute the work to
  -t TMP_DIRECTORY, --temp TMP_DIRECTORY
                        Temporary directory used by pybedtools
  -T THRESHOLD, --threshold THRESHOLD
                        p-value cutoff
  -P PVAL, --pval PVAL  p-value cutoff
  -H HAS_HEADER, --header HAS_HEADER
                        Defines if the circRNA input file has a header line
                        [default: no]
  -F OUTPUT_FILENAME, --output-filename OUTPUT_FILENAME
                        Defines the output file prefix [default: output]

```


