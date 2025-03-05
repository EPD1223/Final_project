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

