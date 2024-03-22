<!-- Installing iq tree
I downlaoded iqtree from the following website 
http:/www.iqtree.org/ i choose the latest release 2.2.2.6 May 27, 2023 -->

<!--i then used the following command to check that installation worked -->
bin/iqtree -s example.phy


<!--i then put it into my software folder in final-project-repository.
i dragged the iqtree into the terminal and then added my alignedfile giving
the following: -->

/Users/robertoregalado/Desktop/final-project-repository/Software/iqtree2 -s /Users/robertoregalado/Desktop/final-project-repository/Data/xylaria_dump_aligned.fasta

<!-- the output reccomended the following DNA model for my fasta file. 
Best-fit model: K2P+I -->

<!-- then i inferred my first phylogeny here -->

/Users/robertoregalado/Desktop/final-project-repository/iqtree2 -s xylaria_dump_aligned.fasta -bb 1000 -nt AUTO

<!-- then i did partition model analysis -->

/Users/robertoregalado/Desktop/final-project-repository/iqtree2 -s xylaria_dump_aligned.fasta -spp xylaria_dump_aligned.nex -bb 1000 -nt AUTO
