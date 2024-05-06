---
Final project reproducible script
--

Section S1 Installations
--
**S1 section 1 - installing MAFFT**
To install Maaft i ran the following code in the terminal
```
sudo port install mafft
```
to confirm that maaft is installed i put the folllowing command into terminal
```
which mafft
```
I got the following output confirming it is installed and in my path
```
/usr/local/bin/mafft
```

**S1 section 2 - installing MUSCLE**
I installed muscle through the homebrew package installer software

**installing homebrew**
I needed to install homebrew to be able to install mrbayes on mac, i went to the following website 
    https://brew.sh/
This website directed me to put the following command into the terminal in the final-project-repository directory
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

This installed homebrew succesfully.

Then i ran these two commands in terminal to add Homebrew to my PATH:
```
    (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/robertoregalado/Desktop/final-project-repository/Software/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
```
the path is as follows
```
 robertoregalado@Keller-lab---robertos-MacBook-Air:~/Desktop/final-project-repository$ brew install muscle
```
Then i installed muscle via hombrew using the following command
```
brew install muscle
```
to confirm that muscle was in fact installed i input the following command
```
muscle -version
```
I received the following
```
MUSCLE v3.8.1551 by Robert C. Edgar
```
**S1 section 3 - installing IqTree2**
Installing iq tree
I downlaoded iqtree from the following website 
```
http:/www.iqtree.org/ 
```

i choose the latest release 2.2.2.6 May 27, 2023 and put it in my data folder in this path
```
/Users/robertoregalado/Desktop/final-project-repository/Software/iqtree2 
```

i then used the following command to check that installation worked
```
./iqtree2 --version
```
i got the folllowing output confirming that this version of iqtree2 is isntalled.
```
Q-TREE multicore version 2.2.2.6 COVID-edition for Mac OS X 64-bit built May 27 2023
Developed by Bui Quang Minh, James Barbetti, Nguyen Lam Tung,
Olga Chernomor, Heiko Schmidt, Dominik Schrempf, Michael Woodhams, Ly Trong Nhan.
```
**S1 section 4 - installing Rstudio**
In order to visualize many of the output files used in this phylogenetic analysis, Rstudio is used. in order to install it to view many of these files i found the intsall link here

```
https://cran.r-project.org/
```
**S1 section 5 - installing MrBayes**
The following commands installed mrbayes while in the software directory after homebrew was installed
```
    brew tap brewsci/bio
    brew install mrbayes
```
To verify that i did, in fact, install mrbayes, i typed the command "mb" into the terminal and it initialized returing the following
```
 "MrBayes 3.2.7a arm
 

                      (Bayesian Analysis of Phylogeny)

                             (Parallel version)
                         (1 processors available)

              Distributed under the GNU General Public License


               Type "help" or "help <command>" for information
                     on the commands that are available.

                   Type "about" for authorship and general
                       information about the program.


MrBayes > "
```

**S1 section 6 - installing tracer**
The download link for tracer can be found here
```
https://beast.community/tracer
```
**Aquiring my data set**
My goal was to do a species tree of several strains/species in the Xylaria genus.  I set out to find a suitable gene that all of the species shared, i settled instead on the ITS non coding region which is universally conserved gene in fungi.

I did a nucleotide blast of accession number AF163036 on ncbi wich returned the ICS gene of many closely related Xylaria species, I will list them here

Xylaria hypoxylon CBS 590.72
Xylaria polymorpha strain NW-FVA2229
Xylaria polymorpha strain DSM 105756
Xylaria polymorpha strain FeC105
Xylaria polymorpha isolate TW07032019_02
Xylaria sp. isolate MBD_3013
Xylaria schweinitzii voucher HMJAU 22751
Xylaria scruposa isolate 866
Xylaria longipes strain NW-FVA2228
Xylaria corniformis MN219591.1

I then downloaded the unaligned fasta files from each of these species and named the file
```
xylaria_muscle.txt
```
Because xylaria is in the family of sordariomyscytes (ascomycete fungi that generally produce perithicial ascocarps) I also downloaded the ITS gene region of Neurospora_cratophora_CBS_558 a closely related sordariomycete species for use an outgroup.

that downlaod can be found here
```
https://www.ncbi.nlm.nih.gov/nuccore/NR_159859.1
```


**Alignment of Files**
In order to Have redundancy, i installed two alignment softwares, the first was muscle and the second was maaft


**Alignment using muscle**
for the purposes of using muscle i named the fasta sequenes i downladed from ncbi in a file named xylaria_muscle.txt and i put it in the following path.

```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle.txt
```
then i duplicated this file and renamed it xylaria_muscle2.txt  I did this so you can still view the original txt file after i convert xylaria_muscle2.txt to a fasta format and use it to align.  I did this using the following command

```
mv xylaria_muscle2.txt xylaria_muscle2.fasta
```
At this point the file was still not aligned, and i added the uniligned sequence from the Neurospora outgroup Then i aligned the file using the following command
```
muscle -in xylaria_muscle2.fasta -out xylaria_muscle2_aligned.fasta
```
This Succesfully produced an aligned file using muscle in the following pathway 
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned.fasta
```


**Aligning Mafft files**
For maaft I aligned the files in the following way
i once again made a duplicate of the following file in my data folder
```
    xylaria_muscle.txt 
```   
The duplicated file was named
```
    xylaria_maaft2.txt
```
I converted this to a fasta file using the following command in the terminal
```
    mv xylaria_maaft2.txt xylaria_maaft2.fasta
```
Then i aligned the file using the following command
```
mafft --auto xylaria_maaft2.fasta > xylaria_maaft2_aligned.fasta
```

This produced an aligned file in the following pathway
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned.fasta
```



**Making Distance and parsimony trees using aligned files from muscle and mafft**

**Using r studio to make distance and parsimony trees**
**For aligned file obtained using muscle**
I loaded the following packages in R
library(stats)
library(ade4)
library(ape)
library(adegenet)
library(phangorn)

Then i converted from fasta to dnabin using the following
```
dna <- fasta2DNAbin(file="/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned.fasta")
D <- dist.dna(dna, model="TN93")
tre <- nj(D)
tre
tre <- ladderize(tre)
plot(tre, cex=.4)
title("Xylaria ITS gene distance tree using muscle")
```
This gave me the following distance tree
![tree_using_muscle](/Users/robertoregalado/Desktop/final-project-repository/Data/Distance_tree_using_muscle.png)

now i will make a parsimony tree withe the following code
```{r}
tre.ini <- nj(dist.dna(dna,model="raw"))
parsimony(tre.ini, dna2)

tre.pars <- optim.parsimony(tre.ini, dna2)
```
<!-- plotting the tree -->
```{r}
plot(tre.pars, cex=0.4) 
title("xylaria muscle tree parsimony")
```
This gave me the following parsimonny tree
![tree_using_muscle](/Users/robertoregalado/Desktop/final-project-repository/Data/Parsimony_tree_using_muscle.png)

I made an rmd file for my Rscript generating these trees, the path is below and i put it in my script folder and named it Xylaria_muscle_aligned_trees.rmd
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/Xylaria_muscle_aligned_trees.Rmd
```

**Using r studio to make distance and parsimony trees**
**For aligned file obtaines using Maaft**



I loaded the following packages in R
```
library(stats)
library(ade4)
library(ape)
library(adegenet)
library(phangorn)
```
Then i converted from fasta to dnabin using the following

```{r}
dna <- fasta2DNAbin(file="/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned.fasta")
D <- dist.dna(dna, model="TN93")
tre <- nj(D)
tre
tre <- ladderize(tre)
plot(tre, cex=.4)
title("Xylaria ITS gene distance tree using maaft")
```

This gave me the following distance tree

![distance_tree_maaft](/Users/robertoregalado/Desktop/final-project-repository/Data/Distance_tree_using_mafft_alignment.png) 

now i will make a parsimony tree withe the following code
```{r}
dna <- fasta2DNAbin(file="/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned.fasta")
dna2 <- as.phyDat(dna)
```
```{r}
tre.ini <- nj(dist.dna(dna,model="raw"))
parsimony(tre.ini, dna2)

tre.pars <- optim.parsimony(tre.ini, dna2)
```
```
``{r}
plot(tre.pars, cex=0.4) 
title("xylaria maaft tree parsimony")
```

This gave me the following parsimony tree
![Parsimony_tree_maaft](/Users/robertoregalado/Desktop/final-project-repository/Data/Parsimony_tree_using_mafft_alignment.png)

I made an rmd file for my Rscript generating these trees the path is here and i put it in my script folder and named them
for muscle
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/Xylaria_muscle_aligned_trees.Rmd
```
For mafft
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/xylaria_mafft_aligned_trees.Rmd
```

**Maximum likelhood section**
**using iqtree on both of my aligned files (muscle and mafft)**

I ran iq tree on my aligned mafft file using the following command
```
/Users/robertoregalado/Desktop/final-project-repository/Software/iqtree2 -s /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned.fasta
```
the output gave me the following recommended model 
```
Best-fit model: TNe+G4 chosen according to BIC
```
I chose the Neurospora cratophora to root my tree with since it is closely related to the xylaria genus, Then i ran the following command with a bootstrap value of 1000 to get the maximum liklyhood tree for my mafft aligned file while in the software directery
```
./iqtree2 -s /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned.fasta -m TNe+G4 -o NR_159859.1 -b 1000
```

The output of this operation gave me a consensus treefile which is viewable in this path
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned.fasta.contree
```

this treefile can be viewed and rooted in R-studio and the script to this can be found at this path
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/Mafft_rooted_tree_IQtree.Rmd
```

A rooted mafft tree image with bootsrap values can be found here
![rooted_tree_maaft](/Users/robertoregalado/Desktop/final-project-repository/Data/Rooted_iqtree2_mafft_BSV.png)



I do the same process with the muscle aligned files in iq tree using this command

running iqtree on aligned muscle file 
```
/Users/robertoregalado/Desktop/final-project-repository/Software/iqtree2 -s /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned.fasta
```

this gave the best fit model as follows
```
Best-fit model: TNe+G4 chosen according to BIC
```
again I chose the Neurospora cratophora to root my tree with since it is closely related to the xylaria genus and ran the following command
```
./iqtree2 -s /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned.fasta -m TNe+G4 -o NR_159859.1 -b 1000 
```
this gave me a consensus tree file at the following path
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned.fasta.contree
```

then i opened Rstudio to visualize the tree file, the path to that file is here
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/Muscle-rooted-iqtree.Rmd
```

thee tree is pictured here
![rooted_tree_muscle](/Users/robertoregalado/Desktop/final-project-repository/Data/Rooted_tree_using_muscle_and_iqtree2_BSV.png)



**Bayesian inference section**
**I made a duplicate copy of my muscle and mafft aligned fasta files to reformat the files in order to eventually turn them into .nex files, the paths for those files are as follows**
**muscle**
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned_copy.fasta
**maaft** 
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_copy.fasta

the process of converting from fasta to nex is documented here in this script file
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/Converting_fasta_to_nex_files.Rmd
```
I initialized mr bayes by typing "mb" in the terminal. and received the following output confirming it was installed
```
MrBayes 3.2.7a arm

                      (Bayesian Analysis of Phylogeny)

                             (Parallel version)
                         (1 processors available)

              Distributed under the GNU General Public License


               Type "help" or "help <command>" for information
                     on the commands that are available.

                   Type "about" for authorship and general
                       information about the program.



```

then i gave the following commands to run Bayesian analysis on both muscle and mafft files

**for mafft**
```
exe /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_end.nex
```
**for muscle**
```
exe /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned_end.nex
```
When i input this command for the maaft file i got this output
```
Executing file "/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_end.nex"
   UNIX line termination
   Longest line length = 355
   Parsing file
   Expecting NEXUS formatted file
   Deleting previously defined characters
   Deleting previously defined taxa
   Reading data block
      Allocated taxon set
      Allocated matrix
      Defining new matrix with 11 taxa and 1002 characters
      Data is Dna
      Missing data coded as ?
      Gaps coded as -
      Data matrix is interleaved
      Taxon  1 -> NR_159859.1_Neurospora_cratophora_CBS_558.94_ITS_region__from_TYPE_material
      Taxon  2 -> MN219591.1_Xylaria_corniformis_small_subunit_ribosomal_RNA_gene__partial_sequence__internal_transc
      Taxon  3 -> MG098261.1_Xylaria_longipes_strain_NW-FVA2228_small_subunit_ribosomal_RNA_gene__partial_sequence__
      Taxon  4 -> KP133498.1_Xylaria_scruposa_isolate_866_18S_ribosomal_RNA_gene__partial_sequence__internal_transcr
      Taxon  5 -> AF163036.1_Xylaria_hypoxylon_CBS_590.72_internal_transcribed_spacer_1__partial_sequence__5.8S_ribo
      Taxon  6 -> JX256828.1_Xylaria_schweinitzii_voucher_HMJAU_22751_18S_ribosomal_RNA_gene__partial_sequence__inte
      Taxon  7 -> MT661488.1_Xylaria_polymorpha_strain_DSM_105756_small_subunit_ribosomal_RNA_gene__partial_sequence
      Taxon  8 -> MG098262.1_Xylaria_polymorpha_strain_NW-FVA2229_small_subunit_ribosomal_RNA_gene__partial_sequence
      Taxon  9 -> MW447065.1_Xylaria_polymorpha_strain_FeC105_18S_ribosomal_RNA_gene__partial_sequence__internal_tra
      Taxon 10 -> MN846336.1_Xylaria_polymorpha_isolate_TW07032019_02_small_subunit_ribosomal_RNA_gene__partial_sequ
      Taxon 11 -> MK595684.1_Xylaria_sp__isolate_MBD_3013_internal_transcribed_spacer_1__partial_sequence__5.8S_ribo
      Successfully read matrix
      Setting default partition (does not divide up characters)
      Setting model defaults
      Seed (for generating default start values) = 401899422
      Setting output file names to "/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_end.nex.<p|t>"
   Exiting data block
   Reading mrbayes block
      Setting autoclose to yes
      Setting Brlenspr to Unconstrained:Exponential(10.00)
      Successfully set prior model parameters
      Setting Shapepr to Exponential(1.00)
      Successfully set prior model parameters
      Setting Tratiopr to Beta(1.00,1.00)
      Successfully set prior model parameters
      Setting Statefreqpr to Dirichlet(1.00,1.00,1.00,1.00)
      Successfully set prior model parameters
      Setting Nst to 2
      Setting Rates to Gamma
      Setting Ngammacat to 4
      Successfully set likelihood model parameters
      Setting number of generations to 1000000
      Setting sample frequency to 10
      Setting print frequency to 100
      Setting number of runs to 1
      Setting number of chains to 3
      Setting chain output file names to "/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_end.nex.<p/t>"
      Successfully set chain parameters
      Setting outgroup to taxon "NR_159859.1_Neurospora_cratophora_CBS_558.94_ITS_region__from_TYPE_material"
   Exiting mrbayes block
   Reached end of file
```
then, for the mafft file i input the following command into mrbayes to perform the Markov chain Monte Carlo anlysis
```
mcmc
```

The analysis was performed succesfully for the mafft file,
this generated the consensus tree.  In order to find out which one of the myriad of trees was the actual consensus tree i put the following command into mrbayes 
```
sumt
```

i repeated the process for the muscle file which also worked succesfully

the output of the mcmc and sumt commands produced several files for both the mafft and muscle alignments including the file in these paths with a nex.con.tre format
**mafft**
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_end.nex.con.tre
```
**muscle**
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned_end.nex.con.tre
```
these files are suitable for viewing in R and show the consensus tree arrived at by the mcmc, i created an r file to display them, the path to that file is here
```
/Users/robertoregalado/Desktop/final-project-repository/Scripts/analyzing_mcmc_nex_dot_t_files.Rmd
```
Images of the consensus trees can be viewed in the following paths

muscle
```
/Users/robertoregalado/Desktop/final-project-repository/Data/Rooted_tree_using_muscle_and_mrbayes.png
```

mafft
```
/Users/robertoregalado/Desktop/final-project-repository/Data/rooted_tree_using_mafft_and_mrbayes.png
```

running MRbayes will usually produce a series of output files, some of which contain the .nex.p format.  These files, display the number of generations run in the MCMC analysis and prove that my MCMC ran for 1000000 generations in both MAFFT and MUSCLE.  These files also can be uploaded into the tracer v1.72 software to assess the mixing and convergance of the mcmc the following are the paths to the .nex.p files for both mafft and muscle 

muscle
```
 /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_muscle2_aligned_end.nex.p
```

mafft
```
/Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_maaft2_aligned_end.nex.p
```

a screenshot of the tracer analysis proving that both MCMC attempts managed to converge
mafft
```
/Users/robertoregalado/Desktop/final-project-repository/Data/Maaft_tracer_output.png
```

muscle
```
/Users/robertoregalado/Desktop/final-project-repository/Data/Muscle_tracer_output.png
```

