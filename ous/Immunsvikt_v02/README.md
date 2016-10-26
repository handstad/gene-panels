*script*
amg origin/dev 91262f1c0b2a9d6b258bac63c54542ca38b41841 (git rev-parse dev)

*Bundle version*
vcpipe-bundle origin/dev 09459ea9dde0a6a939db11bff1d7dd07b693bb26 (git rev-parse dev)

{noformat}
./exe/genepanel --refgene  $REFGENEFILE --dict $DICTFILE --hgmdfile $HGMDFILE --outputdir  /Users/erikseve/tmp/genepanel/immun/ --genepanel=Immun --version=01 --sorter /Users/erikseve/work/amg/src/regions/bedsorter.pl `cat ~/Dropbox/immun-genliste-15062016.txt` 2>&1 | tee /Users/erikseve/tmp/genepanel/immun/script.log
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
TableSet	hsapiens_gene_ensembl	Homo sapiens genes (GRCh37.p13)	1	GRCh37.p13	20050000	default	2016-02-26 15:57:07
{noformat}

Phenotypes manually edited by doctors and then run through the postprocess.py script.
Added transcript/region info for POLE and later renamed to POLE1

# Changes v02
Removed genes/phenotypes. Replaced POLE1 with POLE.

```
sed -i "" -e 's/POLE1/POLE/g' Immunsvikt_v01.phenotypes.csv
sed -i "" -e 's/POLE1/POLE/g' Immunsvikt_v01.transcripts.csv
sed -i "" -e 's/POLE1/POLE/g' Immunsvikt_v01.codingExons.bed
sed -i "" -e 's/POLE1/POLE/g' Immunsvikt_v01.codingExons.slop2.bed
sed -i "" -e 's/POLE1/POLE/g' Immunsvikt_v01.codingExons.slop20.bed
```