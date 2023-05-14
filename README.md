# partialSHIC

Steps involving both a bash and Python file with the same root name are used in conjunction; the bash scripts are examples of how to run the Python software that follow the procedure we performed in our paper for our mosquito study. 

The scripts assume that the GitHub repo is contained within the same local directory, such is the case when downloaded, while training, testing, and empirical data are located within local sub-directories named trainingData/, testingData/, and empiricalData/ respectively. 

Certain data files within the GitHub repo's sub-directory mosquito_data_files/ were too large to upload there, hence the files anc.meru_mela.fa, anc.meru_mela.2L.fa, anc.meru_mela.2R.fa, anc.meru_mela.3L.fa, anc.meru_mela.3R.fa (the preceding five files starting with anc.meru_mela. are all located at http://sesame.uoregon.edu/~adkern/ag1kg_outgroups/), ftp://ngs.sanger.ac.uk/production/ag1000g/phase1/AR3/accessibility/Anopheles-gambiae-PEST_CHROMOSOMES_AgamP3.accessible.fa, AOM_partial_stats.txt, BFM_partial_stats.txt, BFS_partial_stats.txt, CMS_partial_stats.txt, GAS_partial_stats.txt, GNS_partial_stats.txt, GWA_partial_stats.txt, and UGS_partial_stats.txt (the preceding eight files ending in _partial_stats.txt are all located at http://sesame.uoregon.edu/~adkern/ag1kg/shicScanPhaseI/partialStatsAndDafs/) must be downloaded separately into mosquito_data_files/ before running the partialSHIC example run detailed below; within trainingData/ and testingData/, simulations are located across eight directories that have names corresponding to the underlying mosquito population history (e.g. AOM/, BFM/, BFS/, etc.); training simulations can be downloaded from http://sesame.uoregon.edu/~adkern/Xander_kerndev/Detecting_partial_sweeps_Anopheles_mosquito/training_sims_2/; testing simulations can be downloaded from http://sesame.uoregon.edu/~adkern/Xander_kerndev/Detecting_partial_sweeps_Anopheles_mosquito/testing_sims_2/; the command lines used for simulation with the program discoal are provided in a supplemental table from our paper; empirical data can be downloaded from ftp://ngs.sanger.ac.uk/production/ag1000g/phase1/AR3.1/haplotypes/main/hdf5/

Training:
- Convert training simulations, which should be contained within a single file in gzipped ms format per selective sweep class, into two-dimensional matrices (i.e. feature vector images) using training_convert_to_FVs.sh/training_convert_to_FVs.py (**if diploSHIC software has not been previously installed, then the following bash command must be executed beforehand:** python setup.py install; if local install is desired, such as on an HPCC, then the following command may be preferable: python setup.py install --user)
- Sample from simulated feature vector images for equal representation of each selection state during training using training_sample_FVs.sh/training_sample_FVs.py
- (optional) Visualize heatmap of simulated feature vector images for each selection state using training_visualize_FVs.sh
- Train CNN classifier on simulated feature vector images using training_deep_learning.sh/training_deep_learning.py
- (alternative) Train CNN for five-state classification only (i.e. without partial sweeps, or completed sweeps only) on simulated feature vector images using training_deep_learning_5-state-complete-sweeps-only.sh/training_deep_learning_5-state-complete-sweeps-only.py
- (alternative) Train CNN for binary classification only (i.e. between four sweep classes versus without direct selection) on simulated feature vector images using training_deep_learning_binary-selection-presence.sh/training_deep_learning_binary-selection-presence.py

Testing:
- Convert testing simulations, which should be contained within a single file in gzipped ms format per selective sweep class, into two-dimensional matrices (i.e. feature vector images) using testing_convert_to_FVs.sh/testing_convert_to_FVs.py
- Classify simulated test feature vector images with optimized CNN classifier to conduct in silico experiment using testing_deep_learning_classify.sh/testing_deep_learning_classify.py
- (alternative) Classify simulated test feature vector images with optimized CNN five-state classifier to conduct in silico experiment using testing_deep_learning_classify_5-state-complete-sweeps-only.sh/testing_deep_learning_classify_5-state-complete-sweeps-only.py
- (alternative) Classify simulated test feature vector images with optimized CNN binary classifier to conduct in silico experiment using testing_deep_learning_classify_binary-selection-presence.sh/testing_deep_learning_classify_binary-selection-presence.py

Empirical:
- Convert empirical data, which should be in h5 format, into two-dimensional matrices (i.e. feature vector images) using empirical_convert_to_FVs.sh/empirical_convert_to_FVs.py and then empirical_merge_FVs.sh
- Classify empirical feature vector images with optimized CNN classifier using empirical_deep_learning_classify.sh/empirical_deep_learning_classify.py
