## Overview
This file describes how the genepanel files were created.

## Script
amg origin/dev (eb19e4b564dad697edea7471c886341ccddc20e4)

```bash
genepanel \
--refgene  $REFGENEFILE \
--dict $DICTFILE \
--hgmdfile $HGMDFILE \
--outputdir  /Users/erikseve/tmp/genepanel/eeogpu \
--genepanel=EEogPU \
--version=03 \
--sorter /Users/erikseve/work/amg/src/regions/bedsorter.pl \
`cat ~/work/vcpipe-bundle/clinicalGenePanels/EEogPU_v03/EEogPU_v03.genliste.txt` \
2>&1 | tee /Users/erikseve/tmp/genepanel/eeogpu/script.log
```

## Gene list
See attachment.

## Bundle version
vcpipe-bundle  origin/dev (2c29e8cf96eb5f57bab608a2416c149ff83a9e22)

```bash
DICTFILE=/Users/erikseve/work/vcpipe-bundle/genomic/gatkBundle_2.5/human_g1k_v37_decoy.dict;
REFGENEFILE=/Users/erikseve/work/vcpipe-bundle/funcAnnot/refseq/refGene_150311.tsv;
HGMDFILE=/Users/erikseve/Downloads/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf
```

```
vcpipe-bundle/genomic/gatkBundle_2.5/human_g1k_v37_decoy.dict -> ../../.git/annex/objects/mk/F3/SHA256E-s14888--9159a472f08cd79e067bed63a87b13ef73e5f05b8f1e4b4742d24b94821d5424.dict/SHA256E-s14888--9159a472f08cd79e067bed63a87b13ef73e5f05b8f1e4b4742d24b94821d5424.dict
vcpipe-bundle/variantDbs/HGMD/hgmd_all.vcf.gz -> ../../.git/annex/objects/9W/jm/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf.gz/SHA256E-s13329617--d64003b0645089c69f7a27a8b90f6bbc6d352a7a6d3adf47561878a8c08effd7.vcf.gz
vcpipe-bundle/funcAnnot/refseq/refGene_150311.tsv -> ../../.git/annex/objects/vV/8z/SHA256E-s14837856--fa077b870a0f050a4757dee9b6aed58c1a8f22d8277f2487158cebff97c8d11a.tsv/SHA256E-s14837856--fa077b870a0f050a4757dee9b6aed58c1a8f22d8277f2487158cebff97c8d11a.tsv
```

## Review of script log
Interesting output:
Number of gene symbols without phenotypes: 25
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
TableSet        hsapiens_gene_ensembl   Homo sapiens genes (GRCh37.p13) 1       GRCh37.p13      200     50000   default 2016-09-02 14:51:53
```


## Postprocessing
```
python src/genepanel/postprocess.py --transcripts /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/EEogPU_v03/EEogPU_v03draft.transcripts.csv --phenotypes /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/EEogPU_v03/EEogPU_v03draft.phenotypes.KAB --bedfiles /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/EEogPU_v03/EEogPU_v03draft.codingExons.bed /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/EEogPU_v03/EEogPU_v03draft.codingExons.slop2.bed /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/EEogPU_v03/EEogPU_v03draft.codingExons.slop20.bed --outputdir ~/tmp/genepanel/eeogpu
```

Output:

```
Number of transcripts removed: 15
Number of genes in final transcripts file: 852
Number of lines removed from bed file: 236
Number of genes in final bed file: 852
Number of lines removed from bed file: 236
Number of genes in final bed file: 852
Number of lines removed from bed file: 236
Number of genes in final bed file: 852
Number of phenotypes kept: 1259
Number of phenotypes removed: 199
Genes removed by removing phenotypes (15): ABCB7, CAPN10, CASP2, CAV1, CNKSR2, ELP2, FH, HDAC4, KCNH5, KLF8, MTF1, NDNL2, PHF21A, PHIP, SCAPER
Number of genes in final phenotypes file: 852
Genes not in appearing in both transcripts and phenotypes files:
Final panel files are suffixed with 'processed'. They must be renamed manually. See /Users/erikseve/tmp/genepanel/eeogpu
```

Renamed the processed files.

Sorted the phenotypes file.

Renamed panel to PU.

Made ehåndbok attachment:
exe/publish_genepanel /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/PU_v01 ehaandbok > ~/tmp/PU_v01.ehaandbok.csv

Removed genes TUBB2A og TUBB2B:
python src/genepanel/remove_genes.py --symbols TUBB2A,TUBB2B --transcripts $FOLDER/PU_v01.transcripts.csv --phenotypes $FOLDER/PU_v01.phenotypes.csv --bedfiles $FOLDER/PU_v01.codingExons.bed  $FOLDER/PU_v01.codingExons.slop2.bed  $FOLDER/PU_v01.codingExons.slop20.bed --outputdir ~/tmp/genepanel/eeogpu