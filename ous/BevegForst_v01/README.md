exe/genepanel --refgene  $REFGENEFILE --dict $DICTFILE --hgmdfile $HGMDFILE --outputdir  ~/tmp/genepanel/bevegforst  --genepanel=BevegForst --version=01 --sorter /Users/erikseve/work/amg/src/regions/bedsorter.pl `cat /Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/BevegForst_v01/BevegForst_v01_genelist.csv` 2>&1 | tee ~/tmp/genepanel/bevegforst/script.log

 
FOLDER=/Users/erikseve/work/vcpipe-bundle/clinicalGenePanels/BevegForst_v01
python src/genepanel/postprocess.py --transcripts $FOLDER/BevegForst_v01draft.transcripts.csv --phenotypes $FOLDER/BevegForst_v01draft2.phenotypes_20.10.2016_uxwmin_uxnaei --bedfiles $FOLDER/BevegForst_v01draft.codingExons.bed $FOLDER/BevegForst_v01draft.codingExons.slop2.bed $FOLDER/BevegForst_v01draft.codingExons.slop20.bed --outputdir ~/tmp/genepanel/bevegforst
