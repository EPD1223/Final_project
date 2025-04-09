# Final_project

# Alignment steps (with ClustalW):
In terminal run: cd /Users/emmahdaanen/Downloads/FASTA_files
To combine FASTA files run: cat *.fasta > Helianthus_alignment.fasta
  Note: You can change "Helianthus_alignment" to a different name
Open Anaconda Navigator, go to "Environments" tab, and open "base (root)" terminal
  Note: Ensure bioconda and ClustalW are installed
Run: cd /Users/emmahdaanen/Downloads/FASTA_files
To align files run: clustalw2 -INFILE=Helianthus_alignment.fasta -ALIGN -OUTFILE=aligned_sequences.aln

#Distance Based Trees (in R):
Assumptions: The distance between two sequences is the sum of the distances along the path 
connecting them in the tree. Often assumes a constant rate of evolution over time, which may 
not always hold true.
Limitations: Converting sequence data into pairwise distances can result in the loss of 
information about individual character changes. 

Run: library(ape)
     library(phangorn)
Run: setwd("/Users/emmahdaanen/Downloads/FASTA_files")
Build tree: alignment <- read.dna("Helianthus_aligned.aln", format="clustal")
     dist_matrix <- dist.dna(alignment, model="TN93")
     nj_tree <- nj(dist_matrix)
To adjust names on trees run: name_map <- c(
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
To apply name mapping run: nj_tree$tip.label <- name_map[nj_tree$tip.label]
                           plot(nj_tree, main="Distance-Based NJ Tree", cex=.6)
                           write.tree(nj_tree, file="Helianthus_NJ_tree_named.nwk")
                           
#Parsimony-based trees (in R):
Assumptions: Assumes that the simplest explanation, requiring the fewest evolutionary 
changes, is the most likely. Assumes that convergent evolution and parallel evolution.
Limitations: Parsimony is not statistically consistent - meaning it may not always 
produce the correct tree even with large amounts of data. 

Run: library(ape)
     library(phangorn)
Run: setwd("/Users/emmahdaanen/Downloads/FASTA_files")
Build Tree: parsimony_tree <- pratchet(alignment_phyDat)
To adjust names on trees run: name_map <- c(
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
Apply name mapping: parsimony_tree$tip.label <- name_map[parsimony_tree$tip.label]
                    plot(parsimony_tree, main="Parsimony-Based Tree (Renamed)", cex = 0.6)
                    write.tree(parsimony_tree, file="Helianthus_Parsimony_tree_named.nwk")

#Run RAxML 
Assumptions: RAxML assumed that the chosen model of nucleotide or amino acid substitution 
accurately represents the evolutionary process. It assumes that the evolutionary process is
homogeneous across the entire tree, meaning the same model parameters apply to all 
branches. Additionally, sites in the alignment are assumed to evolve independently of each other.
Limitations: RAxML can be computationally intensive, especially for large data sets. 
It has specific ways of handling gaps and missing data, which may not always be ideal
for all data sets. 

Install RAxML
To convert Helianthus_aligned.aln file to PHYLIP format (in terminal) run:
  pip install segmagick
  seqmagick convert Helianthus_aligned.aln Helianthus_aligned.phy 
Use the following command to execute RAxML: 
  raxmlHPC -s Helianthus_aligned.phy -n Helianthus_ML_tree -m GTRGAMMA -p 12345 -# 100
You can visualize the resulting trees using software like FigTree or Dendroscope. 
