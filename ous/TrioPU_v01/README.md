## Overview
This file describes how the genepanel files were created.

## Script
amg origin/dev (b188d031ce18233c183926e5b9cd03eebadaa6d5)

```bash
genepanel \
--refgene  $REFGENEFILE \
--dict $DICTFILE \
--hgmdfile $HGMDFILE \
--outputdir  /Users/erikseve/tmp/genepanel/triopu \
--genepanel=TrioPU \
--version=01 \
--sorter /Users/erikseve/work/amg/src/regions/bedsorter.pl \
`cat /Users/erikseve/TrioPU_genliste_21.01.2016.txt` \
2>&1 | tee /Users/erikseve/tmp/genepanel/triopu/script.log
```

## Gene list
See attachment.

## Bundle version
vcpipe-bundle  origin/master v1.0.2-rel (692fc65859b63b08b4ac2aebaa5b51114047ad4b)

```bash
DICTFILE=/Users/erikseve/work/vcpipe-bundle/genomic/gatkBundle_2.5/human_g1k_v37_decoy.dict;
REFGENEFILE=/Users/erikseve/work/vcpipe-bundle/funcAnnot/refseq/refGene_150311.tsv;
HGMDFILE=/Users/erikseve/Downloads/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf
```

```
vcpipe-bundle/variantDbs/HGMD/hgmd_all.vcf.gz -> ../../.git/annex/objects/9W/jm/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf.gz/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf.gz
vcpipe-bundle/funcAnnot/refseq/refGene_150311.tsv -> ../../.git/annex/objects/vV/8z/SHA256E-s14837856--fa077b870a0f050a4757dee9b6aed58c1a8f22d8277f2487158cebff97c8d11a.tsv/SHA256E-s14837856--fa077b870a0f050a4757dee9b6aed58c1a8f22d8277f2487158cebff97c8d11a.tsv
```

## Review of script log
Interesting output:
- Number of gene symbols without phenotypes: 40
- Symbols not found in Omim
  - sc5d
  - qki,wdr45b
  - lins
  - snx3,prmt10
  - fancm,fbxw4,hdac4,tmem135
  - fry,ralgds
  - eomes,gnptg,tctn1,st3gal5,ywhae
  - tgif1
  - agtr2
  - rgs7,casp2
  - dolk,pecr,inpp4a,srgap3,nkx2-1,ubr7
  - smc1a,nr1i3,mttp,elp2
  - hadh,cnksr1,cnksr2,mapk10,phip,ascc3
  - auts2,eef1b2
  - pdhx

## Ensemble info
```
wget --quiet -O - "http://grch37.ensembl.org/biomart/martservice?type=datasets&mart=ENSEMBL_MART_ENSEMBL" | grep hsapiens_gene_ensembl
TableSet	hsapiens_gene_ensembl	Homo sapiens genes (GRCh37.p13)	1	GRCh37.p13	200	50000	default	2015-11-16 14:47:17
```


## Postprocessing
The postprocess script was run with the inputs
- the automatically created transcripts and bed files
- the phenotypes edited by doctors
The doctors converted the automatically created phenotypes files to an Excel file and added several columns: one to contain an 'X' indicating the phenotypes to be removed, and one containing the PubMed ID. LibreOffice was used to convert the Excel file into a csv file (Excel for Mac messes up newlines and Norwegian characters).

Also the symbol LINS was replaced with LINS1 in the edited phenotypes file. LINS1 is the current HGNC symbol, but not known in grch37. The postprocess script did the same replacment in the transcripts and bed files.

The automatically transcripts and bed files was renamed before the postprocessing as their original name is more suitable for the final genepanel files created by the postprocessing script.
```
python src/genepanel/postprocess.py --phenotypes /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/TrioPU_v01/TrioPU_v01.phenotypes.KEB.LR.030316.csv.txt  --transcripts /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/TrioPU_v01/TrioPU_v01-draft.transcripts.csv --bedfiles `ls /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/TrioPU_v01/*draft*.bed` --replace lins=lins1 --outputdir /Users/erikseve/tmp/processing
```

Finally the output files was renamed to TrioPU_v01.*

## Updates to v01
Replaced LINS1 with LINS, see https://ousamg.atlassian.net/browse/AMG-359

```
sed -i "" -e 's/LINS1/LINS/g' TrioPU_v01.codingExons.bed
sed -i "" -e 's/LINS1/LINS/g' TrioPU_v01.codingExons.slop2.bed
sed -i "" -e 's/LINS1/LINS/g' TrioPU_v01.codingExons.slop20.bed
sed -i "" -e 's/LINS1/LINS/g' TrioPU_v01.transcripts.csv
sed -i "" -e 's/LINS1/LINS/g' TrioPU_v01.phenotypes.csv
```