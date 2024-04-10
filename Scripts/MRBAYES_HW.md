**MRBAYES HW**
**installing homebrew**
I needed to install homebrew to be able to install mrbayes on mac, i went to the following website 
    https://brew.sh/
This website directed me to put the following command into the terminal
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
This installed homebrew succesfully.

Then i ran these two commands in terminal to add Homebrew to my PATH:
    (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/robertoregalado/Desktop/final-project-repository/Software/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"

The following commands then installed mrbayes
    brew tap brewsci/bio
    brew install mrbayes

To verify that i have, in fact, installed mrbayes, i typed the command "mb" into the terminal and it initialized returing the following:
 "MrBayes 3.2.7a arm
 ```

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
I typed "quit" to exit Mr.bayes at this point
I created a nano file from my original aligned fasta file and named it "xylaria_dump_aligned.nex"  to this file i added the following text at the bottom of the file 
    begin mrbayes;
 set autoclose=yes;
 prset brlenspr=unconstrained:exp(10.0);
 prset shapepr=exp(1.0);
 prset tratiopr=beta(1.0,1.0);
 prset statefreqpr=dirichlet(1.0,1.0,1.0,1.0);
 lset nst=2 rates=gamma ngammacat=4;
 mcmcp ngen=10000 samplefreq=10 printfreq=100 nruns=1 nchains=3 savebrlens=yes;
 outgroup MG098261.1 Xylaria longipes strain NW-FVA2228 small subunit ribosomal RNA gene, partial sequence; internal transcribed spacer 1, 5.8S ribosomal RNA gene, and internal transcribed spacer 2, complete sequence; and large subunit ribosomal RNA gene, partial
END;

these commands do the following:
specified that branch lengths are to be unconstrained
specified an exponential distribution with mean 1.0 for the shape parameter of the gamma distribution
Uses a Beta(1,1) distribution as the prior for the transition/transversion rate ratio.
states that a flat Dirichlet distribution is to be used for base frequencies.
tells MrBayes that we would like a 2-parameter substitution matrix
Specifying MCMC options
Specifying "MG098261.1 Xylaria longipes strain NW-FVA2228 small subunit ribosomal RNA gene, partial sequence; internal transcribed spacer 1, 5.8S ribosomal RNA gene, and internal transcribed spacer 2, complete sequence; and large subunit ribosomal RNA gene, partial" as the outgroup.

at this point i reinitalized mrbayes using the "mb" command


I then inputted the following command:
    MrBayes > exe xylaria_dump_aligned.nex
This returned the follwing:
```
Executing file "xylaria_dump_aligned.nex"
   UNIX line termination
   Longest line length = 1056
   Parsing file
   Expecting NEXUS formatted file
   Deleting previously defined characters
   Deleting previously defined taxa
   Reading taxa block
      Allocated taxon set
      Defining new set of 11 taxa
   Exiting taxa block
   Reading characters block
      Allocated matrix
      Defining new character matrix with 986 characters
      Data is Dna
      Gaps coded as -
      Taxon  1 -> Xylaria_hypoxylon_CBS_590.72
      Taxon  2 -> MG098262.1_Xylaria_polymorpha_strain_NW-FVA2229
      Taxon  3 -> MW447065.1_Xylaria_polymorpha_strain_FeC105
      Taxon  4 -> MT661488.1_Xylaria_polymorpha_strain_DSM_105756
      Taxon  5 -> AY909012.1_Xylaria_hypoxylon_strain_CBS_590.72
      Taxon  6 -> MN846336.1_Xylaria_polymorpha_isolate_TW07032019_02
      Taxon  7 -> MK595684.1_Xylaria_sp._isolate_MBD_3013
      Taxon  8 -> JX256828.1_Xylaria_schweinitzii_voucher_HMJAU_22751
      Taxon  9 -> KP133498.1_Xylaria_scruposa_isolate_866
      Taxon 10 -> MG098261.1_Xylaria_longipes_strain_NW-FVA2228
      Taxon 11 -> MN219591.1_Xylaria_corniformis
      Successfully read matrix
      Setting default partition (does not divide up characters)
      Setting model defaults
      Seed (for generating default start values) = 322195881
      Setting output file names to "xylaria_dump_aligned.nex.<p|t>"
   Exiting characters block
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
      Setting chain output file names to "xylaria_dump_aligned.nex.<p/t>"
      Successfully set chain parameters
      Setting outgroup to taxon "MG098261.1_Xylaria_longipes_strain_NW-FVA2228"
   Exiting mrbayes block
   Reached end of file
```
at this point i input the following command:
MrBayes > mcmc
This returned the following after the operation finished:
```
Analysis completed in 60 seconds
   Analysis used 59.67 seconds of CPU time on processor 0
   Log likelihood of best state for "cold" chain was -1968.60

   Acceptance rates for the moves in the "cold" chain:
      With prob.   (last 100)   chain accepted proposals by move
         43.2 %     ( 33 %)     Dirichlet(Tratio)
         25.1 %     ( 28 %)     Dirichlet(Pi)
         27.5 %     ( 33 %)     Slider(Pi)
         71.8 %     ( 49 %)     Multiplier(Alpha)
         37.2 %     ( 33 %)     ExtSPR(Tau,V)
         28.8 %     ( 25 %)     ExtTBR(Tau,V)
         41.9 %     ( 39 %)     NNI(Tau,V)
         37.8 %     ( 44 %)     ParsSPR(Tau,V)
         26.8 %     ( 33 %)     Multiplier(V)
         51.5 %     ( 44 %)     Nodeslider(V)
         25.8 %     ( 24 %)     TLMultiplier(V)

   Chain swap information:

                1       2       3 
        --------------------------
      1 |            0.78    0.59 
      2 |  333469            0.80 
      3 |  333432  333099         

   Upper diagonal: Proportion of successful state exchanges between chains
   Lower diagonal: Number of attempted state exchanges between chains

   Chain information:

     ID -- Heat 
    -----------
      1 -- 1.00  (cold chain)
      2 -- 0.91 
      3 -- 0.83 

   Heat = 1 / (1 + T * (ID - 1))
      (where T = 0.10 is the temperature and ID is the chain number)
```

