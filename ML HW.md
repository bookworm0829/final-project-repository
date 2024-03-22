**Maximum liklyhood HW**

I decided to use iqtree, because it is a good algorithm for maximum liklyhood phylogenies
**Description**
IQ-Tree is a fast and effective stochastic algorithm to infer phylogenetic trees by maximum likelihood

**Software** 
it uses a partitioned directory to bootstrap a file that can be viewed in tree viewer

**Strenghts**
finds higher liklyhood trees than raxml

**weaknesses**
requires longer cpu times than raxml

**assumptions**
alignment length must be at least four (or two) times the number of sequences in DNA (or AA) alignments. 



**Installing iq tree**
I downlaoded iqtree from the following website 
http:/www.iqtree.org/ i choose the latest release 2.2.2.6 May 27, 2023 -->

**I then used the following command to check that installation worked**
bin/iqtree -s example.phy


**I then put it into my software folder in final-project-repository. i dragged the iqtree into the terminal and then added my alignedfile giving the following**

/Users/robertoregalado/Desktop/final-project-repository/Software/iqtree2 -s /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_dump_aligned.fasta

**The output reccomended the following DNA model for my fasta file.** 
Best-fit model: K2P+I -->

**Then i inferred my first phylogeny here**

/Users/robertoregalado/Desktop/final-project-repository/iqtree2 -s xylaria_dump_aligned.fasta -bb 1000 -nt AUTO

**Then i did partition model analysis**

/Users/robertoregalado/Desktop/final-project-repository/iqtree2 -s xylaria_dump_aligned.fasta -spp xylaria_dump_aligned.nex -bb 1000 -nt AUTO
