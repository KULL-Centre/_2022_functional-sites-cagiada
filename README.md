# Discovering functionally important sites in proteins

This repository contains Python code, [Jupyter](http://jupyter.org) Notebooks and used data for reproducing the work of the scientific paper _Discovering functionally important sites in proteins_ by M. Cagiada, S. Bottaro, S. Lindemose, S. M. Schenstrøm, A. Stein, R. Hartmann-Petersen and K. Lindorff-Larsen, 2023, Nature Communications 14 (1): 1–13. [https://doi.org/10.1038/s41467-023-39909-0](https://doi.org/10.1038/s41467-023-39909-0).

## Layout
- `Functional_site_model.ipynb` Jupyter Notebook to process and reproduce all the prediction uses in the paper and make new predictions on novel data.
- `catboost_model` folder which contains the trained Catboost model.
- `scores_GEMME` folder which contains the GEMME scores predicted for the he proteins used in the manuscript.
- `scores_rosetta` folder which contains the rosetta stability predictions predicted scores for the proteins used in the manuscript.
- `scores_RaSP` folder which contains the RaSP stability predictions predicted scores for the proteins used in the manuscript.
- `scores_maves` folder which contains the public available MAVE data from different study to train the model and validate it in the manuscript.
- `score_dssp` folder which contains the measure from DSSP used in the manuscript to analyse complexes of proteins
- `pdbs` folder which contains pdbs used for the proteins used in the manuscript.
- `jupyter_notebooks_analysis_figures_paper` folder which contains the notebooks used to recreate most of the analysis and figures in the manuscript. N.B: Each notebook requires specific packages and data in input, all the datasets to run each notebook are provided in the other folders of this repository.

## Functional Model Notebook
### Usage
To run the Prediction Notebook, we suggest to open it in [Google Colaboratory](https://colab.research.google.com/), it can be open clicking [here](https://colab.research.google.com/github/KULL-Centre/_2022_functional-sites-cagiada/blob/main/Functional_site_model.ipynb).
To run the Notebook is necessary to follow different steps:
1 Run the cells with the PRELIMINARY OPERATIONS prefix, this will install all the dependencies and load the required functions to run the predictor.
2 Upload all the required input for your target protein running all the DATA PREPROCESSING cells. In particular in required to:
  - add the target protein sequence
  - add the file with the thermodynamic stability measure (RaSP or Rosetta).
  - add the file with the evolutionary conservation measure made (GEMME via custom file or webserver, MSA for GEMME can be created following this [notebook](https://colab.research.google.com/github/KULL-Centre/_2022_functional-sites-cagiada/blob/main/MSA_for_GEMMEwebserver.ipynb).
  - add the target protein structure (experimental or PDB) which can cover all the target sequence or part of it. 
3 Run the cell 'Variant prediction and residue classification' to load the model and using it to make predictions with the provided input informations.
4 Run the cell 'Show results'  to generate the calssification heatmaps for variants and residues.
5 Run the cell 'Download predictions'   to download the files with summarised input features, predictions and figures.

### File format:

- The input data should follow, where possible, the same numeration of the uploaded query sequence. In case of different numeration, the pipeline will automatically align the two sequences (query and input file) and run the classification only on matching positions.

- Each input file (conservation scores and stability predictions) should be formatted before uploading.

Here we provide an example of formatting for a protein wuth 45 residues:

********************************* 

Mutation  Score[in kcal/mol]  
M1A       2.4  
M1C       1.2  
..  
M1W       1.3  
C2A       0.2   
..  
..  
Y45W       0.3  
  
********************************* 

N.B.: Synonymous mutations should be skipped or reported as mutation to =. Stop mutations has to been removed from the list.
Examples of prediction files can be found in 'scores_rosetta/scores_GEMME' folder.

- Conservation scores can be generated also using GEMME online website. In this case the sequence used HAS TO MATCH the input query sequence.

- The PBD file should follow the same numeration as the query structure. If this is not possible, the features evaluated on the PDB will be aligned to the query using the alignment between the two sequences.

### Output:
Running  the 'Download predictions' cell generates two output files, which can be downloaded as archive or display online in the colaboratory.
- The first file (named: 'prefix_variant_features.txt') contain a summary of the input features for each variant of the target sequence.
- The second file (named: 'prefix_variant_prediction.txt') contains the model predictions for each single variant of the target protein.
- The third file (named: 'prefix_residue_prediction.txt') instead contains information about the predicted residue class and statistic about variant classes for each residue.
- The folder 'figures' includes all the histogram and heatmaps generated during the run.

### Extra
#### License:

The source code and model's parameters are licensed under the permissive Apache Licence, Version 2.0.

#### Bugs:

For any bugs please report the issue on the project [Github](https://github.com/KULL-Centre/_2022_functional-sites-cagiada) or contact one of the listed authors in the connected [manuscript](https://doi.org/10.1038/s41467-023-39909-0).

#### Citing this work:

If you use our model please cite:

Cagiada, Matteo, Sandro Bottaro, Søren Lindemose, Signe M. Schenstrøm, Amelie Stein, Rasmus Hartmann-Petersen, and Kresten Lindorff-Larsen. 2023. “Discovering Functionally Important Sites in Proteins.” Nature Communications 14 (1): 1–13. https://doi.org/10.1038/s41467-023-39909-0.
```

@ARTICLE{Cagiada2023-pe,
  title     = "Discovering functionally important sites in proteins",
  author    = "Cagiada, Matteo and Bottaro, Sandro and Lindemose, S{\o}ren and
               Schenstr{\o}m, Signe M and Stein, Amelie and Hartmann-Petersen,
               Rasmus and Lindorff-Larsen, Kresten",
  journal   = "Nat. Commun.",
  publisher = "Nature Publishing Group",
  volume    =  14,
  number    =  1,
  pages     = "1--13",
  month     =  jul,
  year      =  2023,
  language  = "en"
}

```
