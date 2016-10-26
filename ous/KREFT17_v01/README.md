~/amg/exe/genepanel --refgene /home/yingsh/vcpipe-bundle/funcAnnot/refseq/refGene_150311.tsv --outputdir /home/yingsh/genepanel/KREFT_v01 --genepanel=KREFT --version=01 --dict /home/yingsh/vcpipe-bundle/genomic/gatkBundle_2.5/human_g1k_v37_decoy.dict --hgmdfile /home/yingsh/vcpipe-bundle/.git/annex/objects/9W/jm/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf.gz/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf --sorter /home/yingsh/amg/src/regions/bedsorter.pl `cat KREFT_underpaneler_v1.txt` 2>&1 | tee script.log

python ~/home/github/amg/src/genepanel/postprocess.py --phenotypes fenotyper_kreft_HTS_TW020316.reformat.1.txt --transcripts KREFT_v01/KREFT_v01.transcripts.csv --bedfiles `ls KREFT_v01/KREFT_v01.*bed` --outputdir KREFT_v01 --subpanel KREFT --version v01 --symbolsfile KREFT_v01/KREFT_underpaneler_v1.txt 
Generating files for subpanel KREFT v01
Number of transcripts removed: 0
Number of genes in final transcripts file: 17
Number of lines removed from bed file: 0
Number of genes in final bed file: 17
Number of lines removed from bed file: 0
Number of genes in final bed file: 17
Number of lines removed from bed file: 0
Number of genes in final bed file: 17
Number of phenotypes kept: 58
Number of phenotypes removed: 25
Genes removed by removing phenotypes (0): 
Number of genes in final phenotypes file: 17
Genes not in appearing in both transcripts and phenotypes files: 
Subpanel files are put in KREFT_v01
