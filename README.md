# Final_project

# Obtain data
35 DNA sequences were obtained from this study: https://doi.org/10.3732/ajb.94.11.1837
The data used in this project specifically:
  1. Helianthus annuus -  DQ486533
  2. Helianthus argophyllus - DQ486536
  3. Helianthus arizonensis - DQ486542
  4. Helianthus atrorubens - DQ486543
  5. Helianthus bolanderi - DQ486545
  6. Helianthus carnosus - DQ486547
  7. Helianthus decapetalus - DQ486557
  8. Helianthus deserticola - DQ486561
  9. Helianthus divaricatus - DQ486563
  10. Helianthus eggertii - DQ486568
  11. Helianthus floridanus - DQ486571
  12. Helianthus gracilentus - DQ486578
  13. Helianthus glaucophyllus - DQ486576
  14. Helianthus grosseserratus - DQ486579
  15. Helianthus hirsutus - DQ486583
  16. Helianthus heterophyllus - DQ486582
  17. Helianthus laciniatus - DQ486585
  18. Helianthus longifolius - DQ486589
  19. Helianthus laevigatus - DQ486587
  20. Helianthus mollis - DQ486595
  21. Helianthus maximiliani - DQ486590
  22. Helianthus microcephalus - DQ486592
  23. Helianthus nuttallii - DQ486598
  24. Helianthus occidentalis - DQ486601
  25. Helianthus pauciflorus - DQ486607
  26. Helianthus praecox - DQ486613
  27. Helianthus pumilus - DQ486614
  28. Helianthus paradoxus - DQ486602
  29. Helianthus radula - DQ486615
  30. Helianthus resinosus - DQ486617
  31. Helianthus silphioides - DQ486623
  32. Helianthus schweinitzii - DQ486621
  33. Helianthus tuberosus - DQ486628
  34. Helianthus verticillatus - DQ486631
  35. Viguiera pringlei - HQ688934
Download all desired FASTA files and store them in one folder. 
    Note: In this project, FASTA files were stores in a folder called "FASTA_files".


# Download Anaconda Navigator
1. Go to the official Anaconda website: https://www.anaconda.com
2. Navigate to the Downloads Page, select your OS, and download the installer. 
3. Run the installer and follow the installation instructions to guide you through the setup. 
4. Launch Anaconda Navigator. 


# Alignment steps (with ClustalW):
1. In terminal, navigate to folder where FASTA files are located. 
2. To combine FASTA files run: cat *.fasta > Helianthus_alignment.fasta
      Note: You can change "Helianthus_alignment" to a different name.
3. Open Anaconda Navigator, go to "Environments" tab, and open "base (root)" terminal.
      Note: Ensure bioconda and ClustalW are installed.
4. In Anaconda Navigator terminal, navigate to the folder where the FASTA files are located. 
5. To align files run: clustalw2 -INFILE=Helianthus_alignment.fasta -ALIGN -OUTFILE=aligned_sequences.aln. 
      Note: Again, you can change the output ("aligned_sequences.aln") to the desired name but keep the ".aln".
6. Ensure FASTA and alignments files are in the same folder. 

#Distance Based Trees (in R):
Assumptions:
  1. The distance between two sequences is the sum of the distances along the path connecting them in the tree.
  2. Often assumes a constant rate of evolution over time, which may not always hold true.
Limitations:
  1. Converting sequence data into pairwise distances can result in the loss of information about individual character changes. 

1. In R run:
    install.packages("ape")
    install.pakages("phangorn")
    library(ape)
    library(phangorn)
2. Navigate to folder where FASTA and alignment files are located. 
3. Build tree by running: 
    alignment <- read.dna("Helianthus_aligned.aln", format="clustal")
    dist_matrix <- dist.dna(alignment, model="TN93")
    nj_tree <- nj(dist_matrix)
4. To adjust names on trees run (you can change the code accordingly based on which species are used): 
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

1. Install R: https://cran.r-project.org
2. Install R studio: https://posit.co/download/rstudio-desktop/ 
3. In R run: 
    library(ape)
    library(phangorn)
4. Navigate to folder with FASTA and alignment files. 
5. Read the alignment file (Clustal format):
    parsimony_alignment <- read.dna("Helianthus_aligned.aln", format = "clustal")
    alignment_phyDat <- phyDat(parsimony_alignment, type = "DNA")
6. Build Tree by running: 
    parsimony_tree <- pratchet(alignment_phyDat)
7. To adjust names on trees run (you can change the code accordingly based on which species are used): 
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
8. Apply name mapping by running: 
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

1. Install RAxML: https://github.com/amkozlov/raxml-ng/releases
2. To convert Helianthus_aligned.aln file to PHYLIP format (in terminal) run:
    pip install segmagick
    seqmagick convert Helianthus_aligned.aln Helianthus_aligned.phy 
3. Use the following command to execute RAxML: 
    raxmlHPC -s Helianthus_aligned.phy -n Helianthus_ML_tree -m GTRGAMMA -p 12345 -# 100
4. You can visualize the resulting trees using software like FigTree or Dendroscope. 
  4.5 RAxML tree can be visualed in R through the following commands (name mapping is optional, see directions above):
      RAxML_tree <- read.tree("RAxML_bestTree.Helianthis_ML_tree")
      RAxML_tree$tip.label <- name_map[RAxML_tree$tip.label]
      plot(RAxML_tree, main="Maximum_Likelihood_RAxML", cex = 0.6)
5. Ensure all files are located in the same folder (with the FASTA and alignment files).


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

1. Install MrBayes: https://github.com/NBISweden/MrBayes
2. Convert Helianthus_aligned.aln file into NEXUS file, use the online tool, Phylogeny.fr,
   and title it "Helianthus_aligned_mrbayes.nex". 
3. If the file does not contain a "BEGIN MRBAYES; ... END;" block, add the following block
    to the end of the file: 
      begin mrbayes;
        set autoclose=yes nowarn=yes;
        lset nst=6 rates=gamma;
        mcmc ngen=1000000 samplefreq=100 printfreq=100 diagnfreq=1000 nchains=4 savebrlens=yes;
        sumt burnin=2500;
      end;
4. Ensure MrBayes and Helianthus_aligned_mrbayes.nex are in the same directory.
5. Launch MrBayes by typing "mb"" in your terminal command line.
6. Load NEXUS file by running: 
    execute Helianthus_aligned_mrbayes.nex
7. Once loaded, MrBayes will start the analysis automatically because of the "begin mrbayes;" block.
8. Let it run until it completes all generations. 
9. In R, build the tree with the following code (name mapping is option, see directions above): 
    MB_tree <- read.nexus("Helianthus_aligned_mrbayes.nex.con.tre")
    MB_tree$tip.label <- ifelse(MB_tree$tip.label %in% names(name_map),
                           name_map[MB_tree$tip.label],
                           MB_tree$tip.label)
    plot(MB_tree, show.node.label = TRUE, cex = 0.6)
    title("Bayesian Inference Tree of Helianthus Species")
