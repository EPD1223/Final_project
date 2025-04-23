# Final_project

# Alignment steps (with ClustalW):
In terminal run:
  cd /Users/emmahdaanen/Downloads/FASTA_files
To combine FASTA files run:
  cat *.fasta > Helianthus_alignment.fasta
    Note: You can change "Helianthus_alignment" to a different name.
Open Anaconda Navigator, go to "Environments" tab, and open "base (root)" terminal.
  Note: Ensure bioconda and ClustalW are installed.
Run: 
  cd /Users/emmahdaanen/Downloads/FASTA_files
To align files run:
  clustalw2 -INFILE=Helianthus_alignment.fasta -ALIGN -OUTFILE=aligned_sequences.aln. 

#Distance Based Trees (in R):
Assumptions:
  1. The distance between two sequences is the sum of the distances along the path connecting them in the tree.
  2. Often assumes a constant rate of evolution over time, which may not always hold true.
Limitations:
  1. Converting sequence data into pairwise distances can result in the loss of information about individual character changes. 

Run: 
  library(ape)
  library(phangorn)
  setwd("/Users/emmahdaanen/Downloads/FASTA_files")
Build tree by running: 
  alignment <- read.dna("Helianthus_aligned.aln", format="clustal")
  dist_matrix <- dist.dna(alignment, model="TN93")
  nj_tree <- nj(dist_matrix)
To adjust names on trees run: 
  name_map <- c(
    "DQ486533.1" = "Helianthus annuus", "DQ486536.1" = "Helianthus argophyllus", 
    "DQ486542.1" = "Helianthus arizonensis", "DQ486543.1" = "Helianthus atrorubens",
    "DQ486545.1" = "Helianthus bolanderi", "DQ486547.1" = "Helianthus carnosus",
    "DQ486557.1" = "Helianthus decapetalus", "DQ486561.1" = "Helianthus deserticola",
    "DQ486563.1" = "Helianthus divaricatus", "DQ486568.1" = "Helianthus eggertii",
    "DQ486571.1" = "Helianthus floridanus", "DQ486578.1" = "Helianthus gracilentus",
    "DQ486576.1" = "Helianthus glaucophyllus", "DQ486579.1" = "Helianthus grosseserratus",
    "DQ486583.1" = "Helianthus hirsutus", "DQ486582.1" = "Helianthus heterophyllus",
    "DQ486585.1" = "Helianthus laciniatus", "DQ486589.1" = "Helianthus longifolius",
    "DQ486587.1" = "Helianthus laevigatus", "DQ486595.1" = "Helianthus mollis",
    "DQ486590.1" = "Helianthus maximiliani", "DQ486592.1" = "Helianthus microcephalus",
    "DQ486598.1" = "Helianthus nuttallii", "DQ486601.1" = "Helianthus occidentalis",
    "DQ486607.1" = "Helianthus pauciflorus", "DQ486613.1" = "Helianthus praecox",
    "DQ486614.1" = "Helianthus pumilus", "DQ486602.1" = "Helianthus paradoxus",
    "DQ486615.1" = "Helianthus radula", "DQ486617.1" = "Helianthus resinosus",
    "DQ486623.1" = "Helianthus silphioides", "DQ486621.1" = "Helianthus schweinitzii",
    "DQ486628.1" = "Helianthus tuberosus", "DQ486631.1" = "Helianthus verticillatus",
    "HQ688934.1" = "Viguiera pringlei") 
To apply name mapping run: 
  nj_tree$tip.label <- name_map[nj_tree$tip.label]
  plot(nj_tree, main="Distance-Based NJ Tree", cex=.6)
  write.tree(nj_tree, file="Helianthus_NJ_tree_named.nwk")
                           
#Parsimony-based trees (in R):
Assumptions:
  1. Assumes that the simplest explanation, requiring the fewest evolutionary changes, is the most likely.
  2. Assumes that convergent evolution and parallel evolution.
Limitations:
  1. Parsimony is not statistically consistent - meaning it may not always produce the correct tree even with large amounts of data. 

Run: 
  library(ape)
  library(phangorn)
  setwd("/Users/emmahdaanen/Downloads/FASTA_files")
Build Tree by running: 
  parsimony_tree <- pratchet(alignment_phyDat)
To adjust names on trees run: 
  name_map <- c(
    "DQ486533.1" = "Helianthus annuus", "DQ486536.1" = "Helianthus argophyllus", 
    "DQ486542.1" = "Helianthus arizonensis", "DQ486543.1" = "Helianthus atrorubens",
    "DQ486545.1" = "Helianthus bolanderi", "DQ486547.1" = "Helianthus carnosus",
    "DQ486557.1" = "Helianthus decapetalus", "DQ486561.1" = "Helianthus deserticola",
    "DQ486563.1" = "Helianthus divaricatus", "DQ486568.1" = "Helianthus eggertii",
    "DQ486571.1" = "Helianthus floridanus", "DQ486578.1" = "Helianthus gracilentus",
    "DQ486576.1" = "Helianthus glaucophyllus", "DQ486579.1" = "Helianthus grosseserratus",
    "DQ486583.1" = "Helianthus hirsutus", "DQ486582.1" = "Helianthus heterophyllus",
    "DQ486585.1" = "Helianthus laciniatus", "DQ486589.1" = "Helianthus longifolius",
    "DQ486587.1" = "Helianthus laevigatus", "DQ486595.1" = "Helianthus mollis",
    "DQ486590.1" = "Helianthus maximiliani", "DQ486592.1" = "Helianthus microcephalus",
    "DQ486598.1" = "Helianthus nuttallii", "DQ486601.1" = "Helianthus occidentalis",
    "DQ486607.1" = "Helianthus pauciflorus", "DQ486613.1" = "Helianthus praecox",
    "DQ486614.1" = "Helianthus pumilus", "DQ486602.1" = "Helianthus paradoxus",
    "DQ486615.1" = "Helianthus radula", "DQ486617.1" = "Helianthus resinosus",
    "DQ486623.1" = "Helianthus silphioides", "DQ486621.1" = "Helianthus schweinitzii",
    "DQ486628.1" = "Helianthus tuberosus", "DQ486631.1" = "Helianthus verticillatus",
    "HQ688934.1" = "Viguiera pringlei") 
Apply name mapping by running: 
  parsimony_tree$tip.label <- name_map[parsimony_tree$tip.label]
  plot(parsimony_tree, main="Parsimony-Based Tree (Renamed)", cex = 0.6)
  write.tree(parsimony_tree, file="Helianthus_Parsimony_tree_named.nwk")

#Run RAxML 
Assumptions:
  1. RAxML assumed that the chosen model of nucleotide or amino acid substitution accurately represents the evolutionary process. 
  2. It assumes that the evolutionary process is homogeneous across the entire tree, meaning the same model parameters apply to all branches. 
  3. Sites in the alignment are assumed to evolve independently of each other.
Limitations:
  1. RAxML can be computationally intensive, especially for large data sets.
  2. It has specific ways of handling gaps and missing data, which may not always be ideal for all data sets. 

Install RAxML
To convert Helianthus_aligned.aln file to PHYLIP format (in terminal) run:
  pip install segmagick
  seqmagick convert Helianthus_aligned.aln Helianthus_aligned.phy 
Use the following command to execute RAxML: 
  raxmlHPC -s Helianthus_aligned.phy -n Helianthus_ML_tree -m GTRGAMMA -p 12345 -# 100
You can visualize the resulting trees using software like FigTree or Dendroscope. 

#Run MrBayes
Assumptions:
  1. MrBayes assumes the model provided accurately reflects how your sequences evolved.
  2. Assumes the posterior probaility distribution reflects the credibility of trees given your data and model.
  3. Assumes the evolutionary process is homogenous aross the tree. 
Limitations:
  1. Bayesian methods are computationally intensive - especially for large data sets.
  2. Priors can influence results if the data is weak or limited. 
  3. Chains main fail to converge or get stuck in local optima.
  4. MrBayes infers relative branch lengths, not divergence times.

Install MrBayes
Convert Helianthus_aligned.aln file into NEXUS file, use the online tool, Phylogeny.fr,
and title it "Helianthus_aligned_mrbayes.nex".
  If the file does not contain a "BEGIN MRBAYES; ... END;" block, add the following block
  to the end of the file: 
    begin mrbayes;
      set autoclose=yes nowarn=yes;
      lset nst=6 rates=gamma;
      mcmc ngen=1000000 samplefreq=100 printfreq=100 diagnfreq=1000 nchains=4 savebrlens=yes;
      sumt burnin=2500;
    end;
Ensure MrBayes and Helianthus_aligned_mrbayes.nex are in the same directory.
Launch MrBayes by typing "mb"" in your terminal command line.
Load NEXUS file by running: 
  execute Helianthus_aligned_mrbayes.nex
Once loaded, MrBayes will start the analysis automatically because of the "begin mrbayes;" block.
Let it run until it completes all generations. 

# Run ASTRAL (with given test data)
Assumptions:
  1. Assumes that the input gene tree are reasonable accurate. Errors in gene tree estimation can affect the accuracy of the species tree. 
  2. Assumes that gene trees are not affected by horizontal gene transfer, which can complicate phylogeny analysis. 
  3. Works with binary trees, assuming that each node splits into exactly two branches. 
Limitations: 
  1. Can be computationally intensive, especially with large data sets - run time can be significant. 
  2. Errors in gene tree estimation can propagate to the species tree, affecting its accuracy.
  3. ASTRAL may struggles with very large data sets, requiring substantial computational resources. 
  
Install the latest version of ASTRAL. You can find it on the GitHub: https://github.com/smirarab/ASTRAL
Open terminal and navigate to ASTRAL directory. 
Run ASTRAL using the following command:
   java -jar astral.5.7.8.jar -i path/to/simulated_primates_5X.10.gene.tre -o path/to/output_species_tree.tre
   ```


