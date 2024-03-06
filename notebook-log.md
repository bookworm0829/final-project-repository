
#for my data i a datasat containing natural product gees in mushrooms
# After installing mafft i gave the following command pasted below in the terminal the InputForTree.faa file contains the raw data and the alignedInputForTree.faa contains the aligned output
(base) robertoregalado@robertos-MacBook-Air Xylaria % mafft --auto InputForTree.faa > alignedInputForTree.faa
# it returned the following which includes the gap penelaty
nthread = 0
nthreadpair = 0
nthreadtb = 0
ppenalty_ex = 0
stacksize: 8176 kb
rescale = 1
Gap Penalty = -1.53, +0.00, +0.00



Making a distance matrix ..
    1 / 95
done.

Constructing a UPGMA tree (efffree=0) ... 
   90 / 95
done.

Progressive alignment 1/2... 
STEP    10 / 94  f
Reallocating..done. *alloclen = 8220
STEP    88 / 94  f
Reallocating..done. *alloclen = 9223
STEP    93 / 94  f
Reallocating..done. *alloclen = 10250
STEP    94 / 94  f
done.

Making a distance matrix from msa.. 
    0 / 95
done.

Constructing a UPGMA tree (efffree=1) ... 
   90 / 95
done.

Progressive alignment 2/2... 
STEP    14 / 94  f
Reallocating..done. *alloclen = 8214
STEP    91 / 94  f
Reallocating..done. *alloclen = 9558
STEP    94 / 94  f
done.

disttbfast (aa) Version 7.520
alg=A, model=BLOSUM62, 1.53, -0.00, -0.00, noshift, amax=0.0
0 thread(s)

rescale = 1
dndpre (aa) Version 7.520
alg=X, model=BLOSUM62, 1.53, +0.12, -0.00, noshift, amax=0.0
0 thread(s)

minimumweight = 0.000010
autosubalignment = 0.000000
nthread = 0
randomseed = 0
blosum 62 / kimura 200
poffset = 0
niter = 2
sueff_global = 0.100000
nadd = 2
rescale = 1

   90 / 95
Segment   1/ 10    1-1075
Segment   2/ 10 1091-1200.   
Segment   3/ 10 1200-1259.   
STEP 002-093-1  identical.   
Converged.

Segment   4/ 10 1259-1282
STEP 002-093-1  identical.   
Converged.

Segment   5/ 10 1282-1343
STEP 002-077-0  identical.   
Converged.

Segment   6/ 10 1343-1406
Segment   7/ 10 1398-1491.   
Segment   8/ 10 1490-1666.   
Segment   9/ 10 1662-1779.   
Segment  10/ 10 1776-7146.   
done 002-001-1  rejected..   
dvtditr (aa) Version 7.520
alg=A, model=BLOSUM62, 1.53, -0.00, -0.00, noshift, amax=0.0
0 thread(s)


Strategy:
 FFT-NS-i (Standard)
 Iterative refinement method (max. 2 iterations)

If unsure which option to use, try 'mafft --auto input > output'.
For more information, see 'mafft --help', 'mafft --man' and the mafft page.

The default gap scoring scheme has been changed in version 7.110 (2013 Oct).
It tends to insert more gaps into gap-rich regions than previous versions.
To disable this change, add the --leavegappyregion option.

#the command robertoregalado@robertos-MacBook-Air Xylaria '% head alignedInputForTree.faa' gave the following output
-------MA-----------------------------------------------SP--
----------------------------------PTALDSFLKCARGDNYWRPAVQLGDD
IWTYGDLDRISTGIALDLEKSFPKPSPTTVSVVTCISTNHPFVIALSLAAWKAGAVFA--
---------PLDPSVP--RN-----------------------------------VLQAM
LANMKPSVIYDAAGVIDGQHSPEGAVIIH-----APFD-TMDTLAATY-TATL-KVEHPA
ILRTDMALYIHTSSATGPHNIKCVPITHEQLGWYCADLVAASVRHIPDGDYQYMRVLGIS
PFAHVMAHIGDLAWTYETSGCYIFPNLAGAQDMAGAALEALLSSNIDVLLSIPFLAGRIK
EAYLATTDSARLVKMDAA--------------LRRLKIWATAGSQADKSFHEWAASLKLA
LFDSLGMTEIGFLFYGPVDLNSGPGYKSDHVACTHAEIRLVDEHGEPSNDSGELIITGKF

#the presence of gaps indicates that alignment has occured
