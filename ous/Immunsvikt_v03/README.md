*script*
amg origin/dev 91262f1c0b2a9d6b258bac63c54542ca38b41841 (git rev-parse dev)

*Bundle version*
vcpipe-bundle origin/dev 25cb6f690bfe7681ce5e8d675dc6b361d18e1553 (git rev-parse dev)

{noformat}
./exe/genepanel --refgene  $REFGENEFILE --dict $DICTFILE --hgmdfile $HGMDFILE --outputdir  /Users/erikseve/tmp/genepanel/immun/ --genepanel=Immun --version=03 --sorter /Users/erikseve/work/amg/src/regions/bedsorter.pl  NFKB1 2>&1 | tee /Users/erikseve/tmp/genepanel/immun/script.log
{noformat}

{noformat}
echo $DICTFILE $REFGENEFILE $HGMDFILE
/Users/erikseve/work/vcpipe-bundle/genomic/gatkBundle_2.5/human_g1k_v37_decoy.dict
/Users/erikseve/work/vcpipe-bundle/funcAnnot/refseq/refGene_150311.tsv
/Users/erikseve/Downloads/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf
{noformat}

*ensembl*
{noformat}
wget --quiet -O - "http://grch37.ensembl.org/biomart/martservice?type=datasets&mart=ENSEMBL_MART_ENSEMBL" | grep hsapiens_gene_ensembl
TableSet	hsapiens_gene_ensembl	Homo sapiens genes (GRCh37.p13)	1	GRCh37.p13	200	50000	default	2016-09-02 14:51:53
{noformat}

# Changes v03
Copied files from v02.
Ran genepanel script with NFKB1 as input.
Manually merged the files with the v02 ones.
