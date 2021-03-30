Improving the protein inference from bottom-up proteomic data using protein identifications from MS1 spectra
-------------------------------------------------------------------------------------------------------------

This repository contains a simple iPython notebook which creates fake protein homologues. These homologues can be used for estimation of efficiency of protein inference algorithms. Additionally, the Swiss-Prot human database extended with fake protein homologues was uploaded. These fake proteins are the target proteins with 1%, 5% and 25% of replaced amino acids. Also, the fake protein databases extended with decoys proteins in either reversed or shuffled forms are uploaded.

Tutorial for usage of MS1 spectra for improving the protein inference algorithms:
----------------------------------------------------------------------------------

Firstly, the DirectMS1 search engine (ms1searchpy) should be installed. Detailed instructions on how to install and use ms1searchpy are provided here: https://github.com/markmipt/ms1searchpy .
 
Simple example of usage is:

    ms1searchpy /home/mark/test.mzML -d /home/mark/sprot_human_with_fakes.fasta -ad 1
    
Comment: “-ad 1” command creates a shuffled decoy database for FDR estimation.

The output of ms1searchpy contains multiple tables and among them is table called *_proteins_full_noexclusion.tsv. This table contains protein scores ("score" column) calculated by DirectMS1 workflow and these scores are used in the algorithm described in the manuscript.

The method was implemented in the Scavager post-search utility in combination with parsimony principle for protein inference. Detailed instructions on how to install and use Scavager are provided here: https://github.com/markmipt/scavager .

Simple example of usage is:

    scavager path_to_pepXML/MZID -ms1 path_to_DirectMS1_proteins_full_noexclusion.tsv

The output of Scavager contains multiple tables and among them is table called *protein_groups.tsv where chosen protein group leaders are marked with column "groupleader". The analysis is done using the extended parsimony algorithm described in the manuscript if "-ms1" option was used. Scavager can be applied to the output of multiple search engines. Currently supported search engines: IdentiPy, X!Tandem, Comet, MSFragger, MSGF+ and Morpheus.

Python implementation of the proposed algorithm:
-------------------------------------------------
This repository contains an iPython notebook with Python function for the proposed method. This function is a realization of algorithms described in the supporting materials for the manuscript. This code is provided mostly for an advanced users and developers who are interested in their own implementation of the proposed algorithm.


Links
------
- Mailing list: markmipt@gmail.com