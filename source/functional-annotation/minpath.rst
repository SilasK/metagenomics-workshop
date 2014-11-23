===============
Predicting metabolic pathways using MinPath
===============
Metabolic pathways are made up of enzymes that catalyze various reactions. Depending on how pathways are defined, they may contain any number of enzymes. A single enzyme may also be part of one or several pathways. One way of predicting metabolic pathways in a sample is to simply consider all the pathways that a set of enzymes are involved in. This may however overestimate pathways, for instance if only a few of the enzymes required for a pathway are annotated in the sample. 

Here we will predict pathways using the program MinPath to get conservative estimate of the pathways present. MinPath only considers the minimum number of pathways required to explain the set of enzymes in the sample. As input, MinPath requires 1) a file with gene identifiers and enzyme numbers, separated by tabs, and 2) a file that links each enzyme to one or several pathways. The first of these we produced above using pattern matching from the PROKKA gff file. The second file exist in two versions, one that links enzymes to pathways defined in the Metacyc database and one that links enzymes to pathways defined in the KEGG database.

Metacyc file

    data/db/metacyc/ec.to.pwy
    
KEGG file

    data/db/kegg/ec.to.pwy

Run MinPath with this command to predict Metacyc pathways

    MinPath1.2.py -any PROKKA.$SAMPLE.ec -map data/db/metacyc/ec.to.pwy -report PROKKA.$SAMPLE.metacyc.minpath

And to predict KEGG pathways

    MinPath1.2.py -any PROKKA.$SAMPLE.ec -map data/db/kegg/ec.to.pwy -report PROKKA.$SAMPLE.kegg.minpath

Take a look at the report files:

    less -S PROKKA.$SAMPLE.metacyc.minpath
    
**Question: How many Metacyc and KEGG pathways did MinPath predict in your sample? How many were predicted if you had counted all possible pathways as being present? (HINT: look for the 'naive' and 'minpath' tags)**